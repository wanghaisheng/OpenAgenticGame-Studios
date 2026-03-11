# SOAP (Scriptable Object Architecture) Common Pitfalls and Troubleshooting

## Overview
This document covers common pitfalls, issues, and troubleshooting strategies when using SOAP (Scriptable Object Architecture) in Unity projects.

## Common Pitfalls

### 1. Serialization Issues

#### Problem: Circular References
**Symptoms**: Infinite loops, serialization errors, crashes
**Cause**: ScriptableObjects referencing each other in circular patterns
**Solution**:
```csharp
[CreateAssetMenu(fileName = "GameData", menuName = "SOAP/Game Data")]
public class GameData : ScriptableObject
{
    [System.NonSerialized] private bool isInitializing = false;
    
    [SerializeField] private List<RelatedData> relatedData;
    
    private void OnEnable()
    {
        if (!isInitializing)
        {
            isInitializing = true;
            InitializeData();
            isInitializing = false;
        }
    }
    
    private void InitializeData()
    {
        // Safe initialization without circular references
        foreach (var data in relatedData)
        {
            if (data != null && !data.IsInitialized())
            {
                data.Initialize(this);
            }
        }
    }
}
```

#### Problem: Complex Data Types Not Serializing
**Symptoms**: Data loss after play mode, null references
**Cause**: Unity can't serialize certain data types
**Solution**:
```csharp
[CreateAssetMenu(fileName = "ComplexData", menuName = "SOAP/Complex Data")]
public class ComplexData : ScriptableObject
{
    [SerializeField] private SerializableDictionary<string, object> data;
    
    [System.Serializable]
    public class SerializableDictionary<TKey, TValue>
    {
        public List<TKey> keys;
        public List<TValue> values;
        
        public TValue GetValue(TKey key)
        {
            int index = keys.IndexOf(key);
            return index >= 0 ? values[index] : default(TValue);
        }
        
        public void SetValue(TKey key, TValue value)
        {
            int index = keys.IndexOf(key);
            if (index >= 0)
            {
                values[index] = value;
            }
            else
            {
                keys.Add(key);
                values.Add(value);
            }
        }
    }
}
```

#### Problem: ScriptableObject Instance Loss
**Symptoms**: References become null after scene changes
**Cause**: ScriptableObjects not properly loaded
**Solution**:
```csharp
public class ScriptableObjectManager : MonoBehaviour
{
    private static ScriptableObjectManager instance;
    
    [SerializeField] private List<ScriptableObject> scriptableObjects;
    private Dictionary<System.Type, ScriptableObject> objectCache;
    
    private void Awake()
    {
        if (instance == null)
        {
            instance = this;
            DontDestroyOnLoad(gameObject);
            InitializeCache();
        }
        else
        {
            Destroy(gameObject);
        }
    }
    
    private void InitializeCache()
    {
        objectCache = new Dictionary<System.Type, ScriptableObject>();
        foreach (var obj in scriptableObjects)
        {
            if (obj != null)
            {
                objectCache[obj.GetType()] = obj;
            }
        }
    }
    
    public static T GetScriptableObject<T>() where T : ScriptableObject
    {
        if (instance != null && instance.objectCache.TryGetValue(typeof(T), out var obj))
        {
            return obj as T;
        }
        return null;
    }
}
```

### 2. Memory Management Issues

#### Problem: Memory Leaks
**Symptoms**: Memory usage increases over time
**Cause**: Event listeners not properly unsubscribed
**Solution**:
```csharp
[CreateAssetMenu(fileName = "SafeGameEvent", menuName = "SOAP/Safe Game Event")]
public class SafeGameEvent : ScriptableObject
{
    private readonly List<IGameEventListener> listeners = new List<IGameEventListener>();
    
    public void Raise()
    {
        // Create a copy to avoid modification during iteration
        var listenersCopy = new List<IGameEventListener>(listeners);
        
        foreach (var listener in listenersCopy)
        {
            try
            {
                listener.OnEventRaised();
            }
            catch (System.Exception e)
            {
                Debug.LogError($"Error in event listener: {e.Message}");
                // Remove problematic listener
                listeners.Remove(listener);
            }
        }
    }
    
    public void RegisterListener(IGameEventListener listener)
    {
        if (listener != null && !listeners.Contains(listener))
        {
            listeners.Add(listener);
        }
    }
    
    public void UnregisterListener(IGameEventListener listener)
    {
        listeners.Remove(listener);
    }
    
    // Cleanup method
    public void ClearAllListeners()
    {
        listeners.Clear();
    }
    
    private void OnDestroy()
    {
        ClearAllListeners();
    }
}

public interface IGameEventListener
{
    void OnEventRaised();
}
```

#### Problem: Large Data Sets Performance
**Symptoms**: Slow loading times, high memory usage
**Cause**: Large ScriptableObjects loaded entirely at once
**Solution**:
```csharp
[CreateAssetMenu(fileName = "ChunkedData", menuName = "SOAP/Chunked Data")]
public class ChunkedData : ScriptableObject
{
    [SerializeField] private DataChunk[] chunks;
    [SerializeField] private int itemsPerChunk = 100;
    
    [System.Serializable]
    public class DataChunk
    {
        public string[] data;
        [System.NonSerialized] public bool isLoaded = false;
    }
    
    public string GetData(int index)
    {
        int chunkIndex = index / itemsPerChunk;
        int itemIndex = index % itemsPerChunk;
        
        if (chunkIndex >= chunks.Length)
            return null;
            
        LoadChunk(chunkIndex);
        return chunks[chunkIndex].data[itemIndex];
    }
    
    private void LoadChunk(int chunkIndex)
    {
        if (!chunks[chunkIndex].isLoaded)
        {
            // Simulate loading from disk or database
            chunks[chunkIndex].isLoaded = true;
        }
    }
    
    private void UnloadChunk(int chunkIndex)
    {
        if (chunks[chunkIndex].isLoaded)
        {
            chunks[chunkIndex].isLoaded = false;
        }
    }
}
```

### 3. Runtime Data Issues

#### Problem: Runtime Data Being Serialized
**Symptoms**: Play mode changes persisting unexpectedly
**Cause**: Runtime data accidentally marked as [SerializeField]
**Solution**:
```csharp
[CreateAssetMenu(fileName = "RuntimeSafeData", menuName = "SOAP/Runtime Safe Data")]
public class RuntimeSafeData : ScriptableObject
{
    [Header("Serialized Data")]
    public string configName;
    public float defaultValue = 100f;
    
    [Header("Runtime Data - Not Serialized")]
    [System.NonSerialized]
    public float currentValue;
    
    [System.NonSerialized]
    public bool isInitialized = false;
    
    private void OnEnable()
    {
        ResetRuntimeData();
    }
    
    private void OnDisable()
    {
        ResetRuntimeData();
    }
    
    private void ResetRuntimeData()
    {
        currentValue = defaultValue;
        isInitialized = false;
    }
    
    public void Initialize()
    {
        if (!isInitialized)
        {
            currentValue = defaultValue;
            isInitialized = true;
        }
    }
}
```

#### Problem: Shared State Between Instances
**Symptoms**: Changes in one scene affect another
**Cause**: ScriptableObjects sharing global state
**Solution**:
```csharp
[CreateAssetMenu(fileName = "IsolatedData", menuName = "SOAP/Isolated Data")]
public class IsolatedData : ScriptableObject
{
    [System.Serializable]
    public class SceneData
    {
        public string sceneName;
        public float sceneSpecificValue;
        public bool isSceneActive = false;
    }
    
    [SerializeField] private List<SceneData> sceneDataList;
    private Dictionary<string, SceneData> sceneDataMap;
    
    private void OnEnable()
    {
        InitializeSceneDataMap();
    }
    
    private void InitializeSceneDataMap()
    {
        sceneDataMap = new Dictionary<string, SceneData>();
        foreach (var data in sceneDataList)
        {
            sceneDataMap[data.sceneName] = data;
        }
    }
    
    public float GetSceneValue(string sceneName)
    {
        if (sceneDataMap.TryGetValue(sceneName, out var data))
        {
            return data.sceneSpecificValue;
        }
        return 0f;
    }
    
    public void SetSceneValue(string sceneName, float value)
    {
        if (sceneDataMap.TryGetValue(sceneName, out var data))
        {
            data.sceneSpecificValue = value;
        }
        else
        {
            var newData = new SceneData { sceneName = sceneName, sceneSpecificValue = value };
            sceneDataList.Add(newData);
            sceneDataMap[sceneName] = newData;
        }
    }
}
```

### 4. Editor and Build Issues

#### Problem: ScriptableObject References Lost in Build
**Symptoms**: Null references in built game
**Cause**: Resources folder structure issues
**Solution**:
```csharp
public class ScriptableObjectReferenceValidator : MonoBehaviour
{
    [SerializeField] private ScriptableObject[] scriptableObjects;
    
    private void OnValidate()
    {
        ValidateReferences();
    }
    
    private void ValidateReferences()
    {
        for (int i = 0; i < scriptableObjects.Length; i++)
        {
            if (scriptableObjects[i] == null)
            {
                Debug.LogWarning($"ScriptableObject reference {i} is null!");
            }
            else if (!IsInResourcesFolder(scriptableObjects[i]))
            {
                Debug.LogWarning($"ScriptableObject {scriptableObjects[i].name} is not in Resources folder!");
            }
        }
    }
    
    private bool IsInResourcesFolder(ScriptableObject obj)
    {
        string path = AssetDatabase.GetAssetPath(obj);
        return path.Contains("/Resources/");
    }
    
    [ContextMenu("Validate All References")]
    public void ValidateAllReferences()
    {
        ValidateReferences();
    }
}
```

#### Problem: Data Corruption
**Symptoms**: Invalid data, crashes, unexpected behavior
**Cause**: Manual editing of ScriptableObject files
**Solution**:
```csharp
[CreateAssetMenu(fileName = "ValidatedData", menuName = "SOAP/Validated Data")]
public class ValidatedData : ScriptableObject
{
    [SerializeField] private int minValue = 0;
    [SerializeField] private int maxValue = 100;
    [SerializeField] private string requiredField = "";
    
    private void OnValidate()
    {
        ValidateData();
    }
    
    private void ValidateData()
    {
        // Validate numeric ranges
        if (minValue < 0)
        {
            minValue = 0;
            Debug.LogWarning("Min value cannot be negative. Reset to 0.");
        }
        
        if (maxValue < minValue)
        {
            maxValue = minValue;
            Debug.LogWarning("Max value cannot be less than min value. Reset to min value.");
        }
        
        // Validate required fields
        if (string.IsNullOrEmpty(requiredField))
        {
            Debug.LogWarning("Required field cannot be empty!");
        }
        
        // Validate data integrity
        if (minValue > maxValue)
        {
            Debug.LogError("Data integrity error: min > max!");
        }
    }
    
    public bool IsValid()
    {
        return minValue >= 0 && 
               maxValue >= minValue && 
               !string.IsNullOrEmpty(requiredField);
    }
}
```

## Debugging Tools

### 1. ScriptableObject Inspector
```csharp
#if UNITY_EDITOR
using UnityEditor;
[CustomEditor(typeof(ScriptableObject), true)]
public class ScriptableObjectInspector : Editor
{
    public override void OnInspectorGUI()
    {
        DrawDefaultInspector();
        
        if (target is ScriptableObject scriptableObject)
        {
            EditorGUILayout.Space();
            EditorGUILayout.LabelField("Debug Information", EditorStyles.boldLabel);
            
            // Show asset path
            string path = AssetDatabase.GetAssetPath(scriptableObject);
            EditorGUILayout.LabelField("Asset Path", path);
            
            // Show if in Resources folder
            bool inResources = path.Contains("/Resources/");
            EditorGUILayout.LabelField("In Resources", inResources.ToString());
            
            // Show runtime data
            EditorGUILayout.LabelField("Runtime Data", EditorStyles.boldLabel);
            var fields = scriptableObject.GetType().GetFields(
                System.Reflection.BindingFlags.Public | 
                System.Reflection.BindingFlags.NonPublic | 
                System.Reflection.BindingFlags.Instance
            );
            
            foreach (var field in fields)
            {
                if (field.IsDefined(typeof(System.NonSerialized), false))
                {
                    object value = field.GetValue(scriptableObject);
                    EditorGUILayout.LabelField($"{field.Name}", value?.ToString() ?? "null");
                }
            }
            
            // Validation button
            if (GUILayout.Button("Validate Data"))
            {
                ValidateScriptableObject(scriptableObject);
            }
        }
    }
    
    private void ValidateScriptableObject(ScriptableObject obj)
    {
        EditorUtility.SetDirty(obj);
        Debug.Log($"Validated {obj.name}");
    }
}
#endif
```

### 2. Runtime Debugger
```csharp
public class ScriptableObjectDebugger : MonoBehaviour
{
    [SerializeField] private bool enableDebugging = false;
    [SerializeField] private ScriptableObject[] targetObjects;
    
    private void Update()
    {
        if (enableDebugging && Input.GetKeyDown(KeyCode.F1))
        {
            LogAllScriptableObjects();
        }
    }
    
    private void LogAllScriptableObjects()
    {
        Debug.Log("=== ScriptableObject Debug Info ===");
        
        foreach (var obj in targetObjects)
        {
            if (obj != null)
            {
                LogScriptableObjectInfo(obj);
            }
        }
    }
    
    private void LogScriptableObjectInfo(ScriptableObject obj)
    {
        Debug.Log($"--- {obj.name} ({obj.GetType().Name}) ---");
        
        var fields = obj.GetType().GetFields(
            System.Reflection.BindingFlags.Public | 
            System.Reflection.BindingFlags.Instance
        );
        
        foreach (var field in fields)
        {
            object value = field.GetValue(obj);
            Debug.Log($"{field.Name}: {value}");
        }
    }
}
```

## Best Practices Checklist

### Before Implementation
- [ ] Define clear data structure boundaries
- [ ] Plan for serialization requirements
- [ ] Consider memory implications
- [ ] Design for data validation

### During Implementation
- [ ] Use proper serialization attributes
- [ ] Mark runtime data as [System.NonSerialized]
- [ ] Implement data validation
- [ ] Add error handling

### After Implementation
- [ ] Test serialization/deserialization
- [ ] Verify memory usage
- [ ] Test with different platforms
- [ ] Validate data integrity

### Maintenance
- [ ] Regular data validation checks
- [ ] Monitor memory usage
- [ ] Update for Unity version changes
- [ ] Keep documentation current

## Troubleshooting Flowchart

1. **Data not persisting?**
   - Check serialization attributes
   - Verify [System.NonSerialized] usage
   - Test with different data types
   - Check Resources folder structure

2. **Performance issues?**
   - Profile memory usage
   - Check for circular references
   - Implement lazy loading
   - Optimize data structures

3. **Null references?**
   - Verify asset paths
   - Check Resources folder
   - Test in build
   - Validate references

4. **Runtime errors?**
   - Check event subscriptions
   - Validate data types
   - Test error handling
   - Verify initialization order

---

*SOAP Pitfalls and Troubleshooting*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
