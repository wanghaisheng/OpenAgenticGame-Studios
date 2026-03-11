# SOAP (Scriptable Object Architecture) Usage Patterns

## Overview
SOAP provides a robust architecture for managing game data through ScriptableObjects, enabling data-driven design and runtime configuration.

## Core Patterns

### 1. Data Container Pattern
```csharp
[CreateAssetMenu(fileName = "GameData", menuName = "SOAP/Game Data")]
public class GameData : ScriptableObject
{
    [Header("Basic Settings")]
    public string gameName;
    public string version;
    public string description;
    
    [Header("Game Balance")]
    public float baseHealth = 100f;
    public float baseDamage = 10f;
    public float baseSpeed = 5f;
    
    [Header("Progression")]
    public int maxLevel = 100;
    public AnimationCurve experienceCurve;
    
    // Runtime data (not serialized)
    [System.NonSerialized]
    public int currentLevel = 1;
    [System.NonSerialized]
    public float currentExperience = 0f;
    
    public void Initialize()
    {
        currentLevel = 1;
        currentExperience = 0f;
    }
    
    public void AddExperience(float amount)
    {
        currentExperience += amount;
        float requiredExp = GetExperienceForLevel(currentLevel + 1);
        
        while (currentExperience >= requiredExp && currentLevel < maxLevel)
        {
            currentExperience -= requiredExp;
            currentLevel++;
            requiredExp = GetExperienceForLevel(currentLevel + 1);
        }
    }
    
    public float GetExperienceForLevel(int level)
    {
        return experienceCurve.Evaluate(level);
    }
}
```

### 2. Event System Pattern
```csharp
[CreateAssetMenu(fileName = "GameEvent", menuName = "SOAP/Game Event")]
public class GameEvent : ScriptableObject
{
    private List<GameEventListener> listeners = new List<GameEventListener>();
    
    public void Raise()
    {
        for (int i = listeners.Count - 1; i >= 0; i--)
        {
            listeners[i].OnEventRaised();
        }
    }
    
    public void RegisterListener(GameEventListener listener)
    {
        if (!listeners.Contains(listener))
        {
            listeners.Add(listener);
        }
    }
    
    public void UnregisterListener(GameEventListener listener)
    {
        if (listeners.Contains(listener))
        {
            listeners.Remove(listener);
        }
    }
}

public class GameEventListener : MonoBehaviour
{
    public GameEvent gameEvent;
    public UnityEvent response;
    
    private void OnEnable()
    {
        gameEvent.RegisterListener(this);
    }
    
    private void OnDisable()
    {
        gameEvent.UnregisterListener(this);
    }
    
    public void OnEventRaised()
    {
        response.Invoke();
    }
}
```

### 3. Configuration Manager Pattern
```csharp
[CreateAssetMenu(fileName = "GameConfig", menuName = "SOAP/Game Configuration")]
public class GameConfiguration : ScriptableObject
{
    [Header("Audio Settings")]
    public AudioConfiguration audioConfig;
    
    [Header("Graphics Settings")]
    public GraphicsConfiguration graphicsConfig;
    
    [Header("Input Settings")]
    public InputConfiguration inputConfig;
    
    [Header("Gameplay Settings")]
    public GameplayConfiguration gameplayConfig;
    
    public void LoadConfiguration()
    {
        audioConfig.LoadSettings();
        graphicsConfig.LoadSettings();
        inputConfig.LoadSettings();
        gameplayConfig.LoadSettings();
    }
    
    public void SaveConfiguration()
    {
        audioConfig.SaveSettings();
        graphicsConfig.SaveSettings();
        inputConfig.SaveSettings();
        gameplayConfig.SaveSettings();
    }
}

[System.Serializable]
public class AudioConfiguration
{
    [Range(0f, 1f)] public float masterVolume = 1f;
    [Range(0f, 1f)] public float musicVolume = 0.8f;
    [Range(0f, 1f)] public float sfxVolume = 0.9f;
    public bool enableAudio = true;
    
    public void LoadSettings()
    {
        masterVolume = PlayerPrefs.GetFloat("Audio_MasterVolume", masterVolume);
        musicVolume = PlayerPrefs.GetFloat("Audio_MusicVolume", musicVolume);
        sfxVolume = PlayerPrefs.GetFloat("Audio_SFXVolume", sfxVolume);
        enableAudio = PlayerPrefs.GetInt("Audio_EnableAudio", 1) == 1;
    }
    
    public void SaveSettings()
    {
        PlayerPrefs.SetFloat("Audio_MasterVolume", masterVolume);
        PlayerPrefs.SetFloat("Audio_MusicVolume", musicVolume);
        PlayerPrefs.SetFloat("Audio_SFXVolume", sfxVolume);
        PlayerPrefs.SetInt("Audio_EnableAudio", enableAudio ? 1 : 0);
    }
}
```

### 4. Item Database Pattern
```csharp
[CreateAssetMenu(fileName = "ItemDatabase", menuName = "SOAP/Item Database")]
public class ItemDatabase : ScriptableObject
{
    [SerializeField] private List<ItemData> items = new List<ItemData>();
    private Dictionary<string, ItemData> itemDictionary;
    
    private void OnEnable()
    {
        itemDictionary = new Dictionary<string, ItemData>();
        foreach (var item in items)
        {
            if (!itemDictionary.ContainsKey(item.itemID))
            {
                itemDictionary.Add(item.itemID, item);
            }
        }
    }
    
    public ItemData GetItem(string itemID)
    {
        return itemDictionary.TryGetValue(itemID, out var item) ? item : null;
    }
    
    public List<ItemData> GetItemsByType(ItemType type)
    {
        return items.FindAll(item => item.itemType == type);
    }
    
    public bool ContainsItem(string itemID)
    {
        return itemDictionary.ContainsKey(itemID);
    }
}

[CreateAssetMenu(fileName = "ItemData", menuName = "SOAP/Item Data")]
public class ItemData : ScriptableObject
{
    public string itemID;
    public string itemName;
    public string description;
    public Sprite icon;
    public GameObject prefab;
    public ItemType itemType;
    public int stackSize = 1;
    public int value = 0;
    
    [Header("Stats")]
    public int damage = 0;
    public int defense = 0;
    public float speedBonus = 0f;
    
    [Header("Usage")]
    public bool consumable = false;
    public bool equippable = false;
    public GameObject effectPrefab;
}

public enum ItemType
{
    Weapon,
    Armor,
    Consumable,
    Material,
    Quest
}
```

### 5. Level Data Pattern
```csharp
[CreateAssetMenu(fileName = "LevelData", menuName = "SOAP/Level Data")]
public class LevelData : ScriptableObject
{
    [Header("Level Info")]
    public string levelName;
    public string sceneName;
    public Texture2D levelPreview;
    public string description;
    
    [Header("Requirements")]
    public int requiredLevel = 1;
    public List<ItemData> requiredItems;
    
    [Header("Settings")]
    public float timeLimit = 0f; // 0 = no limit
    public int maxLives = 3;
    public bool allowRespawn = true;
    
    [Header("Objectives")]
    public List<LevelObjective> objectives;
    
    [Header("Rewards")]
    public int experienceReward = 100;
    public List<ItemData> itemRewards;
    public int goldReward = 0;
    
    public bool CanStartLevel(PlayerData playerData)
    {
        if (playerData.level < requiredLevel)
            return false;
            
        foreach (var requiredItem in requiredItems)
        {
            if (!playerData.inventory.HasItem(requiredItem.itemID, requiredItem.stackSize))
                return false;
        }
        
        return true;
    }
}

[System.Serializable]
public class LevelObjective
{
    public string objectiveID;
    public string description;
    public ObjectiveType type;
    public string targetID;
    public int requiredAmount = 1;
    public bool isOptional = false;
    
    [HideInInspector] public int currentAmount = 0;
    [HideInInspector] public bool isCompleted = false;
}

public enum ObjectiveType
{
    KillEnemies,
    CollectItems,
    ReachLocation,
    SurviveTime,
    DefendTarget
}
```

## Advanced Patterns

### 1. Runtime State Manager
```csharp
[CreateAssetMenu(fileName = "GameState", menuName = "SOAP/Game State")]
public class GameState : ScriptableObject
{
    [Header("Persistent Data")]
    public PlayerData currentPlayer;
    public GameConfiguration config;
    public List<LevelData> completedLevels;
    
    [Header("Runtime Data")]
    [System.NonSerialized] public bool isPaused = false;
    [System.NonSerialized] public bool isGameOver = false;
    [System.NonSerialized] public float gameTime = 0f;
    
    public event System.Action OnGamePaused;
    public event System.Action OnGameResumed;
    public event System.Action OnGameOver;
    public event System.Action OnLevelCompleted;
    
    public void InitializeGame()
    {
        isPaused = false;
        isGameOver = false;
        gameTime = 0f;
        
        if (currentPlayer != null)
        {
            currentPlayer.Initialize();
        }
    }
    
    public void PauseGame()
    {
        if (!isPaused)
        {
            isPaused = true;
            Time.timeScale = 0f;
            OnGamePaused?.Invoke();
        }
    }
    
    public void ResumeGame()
    {
        if (isPaused)
        {
            isPaused = false;
            Time.timeScale = 1f;
            OnGameResumed?.Invoke();
        }
    }
    
    public void GameOver()
    {
        isGameOver = true;
        OnGameOver?.Invoke();
    }
    
    public void CompleteLevel(LevelData level)
    {
        if (!completedLevels.Contains(level))
        {
            completedLevels.Add(level);
            OnLevelCompleted?.Invoke();
        }
    }
}
```

### 2. Localization Manager
```csharp
[CreateAssetMenu(fileName = "LocalizationData", menuName = "SOAP/Localization Data")]
public class LocalizationData : ScriptableObject
{
    [System.Serializable]
    public class LocalizationEntry
    {
        public string key;
        public string[] translations; // Index matches language enum
    }
    
    public List<LocalizationEntry> entries;
    public SystemLanguage defaultLanguage = SystemLanguage.English;
    
    private Dictionary<string, string[]> translationDictionary;
    
    private void OnEnable()
    {
        translationDictionary = new Dictionary<string, string[]>();
        foreach (var entry in entries)
        {
            translationDictionary[entry.key] = entry.translations;
        }
    }
    
    public string GetTranslation(string key, SystemLanguage language)
    {
        if (!translationDictionary.TryGetValue(key, out var translations))
        {
            return $"Missing: {key}";
        }
        
        int languageIndex = (int)language;
        if (languageIndex >= 0 && languageIndex < translations.Length)
        {
            return translations[languageIndex];
        }
        
        return translations[(int)defaultLanguage];
    }
    
    public string GetTranslation(string key)
    {
        return GetTranslation(key, Application.systemLanguage);
    }
}
```

### 3. Save System Pattern
```csharp
[CreateAssetMenu(fileName = "SaveData", menuName = "SOAP/Save Data")]
public class SaveData : ScriptableObject
{
    [Header("Player Data")]
    public string playerName;
    public int playerLevel;
    public float playerExperience;
    public Vector3 playerPosition;
    public List<string> playerInventory;
    
    [Header("Game Progress")]
    public List<string> completedLevels;
    public List<string> unlockedItems;
    public Dictionary<string, bool> flags;
    
    [Header("Settings")]
    public float masterVolume = 1f;
    public float musicVolume = 0.8f;
    public float sfxVolume = 0.9f;
    public int graphicsQuality = 2;
    
    public void SaveToFile(string fileName)
    {
        string jsonData = JsonUtility.ToJson(this, true);
        string filePath = Path.Combine(Application.persistentDataPath, $"{fileName}.save");
        File.WriteAllText(filePath, jsonData);
    }
    
    public void LoadFromFile(string fileName)
    {
        string filePath = Path.Combine(Application.persistentDataPath, $"{fileName}.save");
        if (File.Exists(filePath))
        {
            string jsonData = File.ReadAllText(filePath);
            JsonUtility.FromJsonOverwrite(jsonData, this);
        }
    }
    
    public void ClearData()
    {
        playerName = "";
        playerLevel = 1;
        playerExperience = 0f;
        playerPosition = Vector3.zero;
        playerInventory = new List<string>();
        completedLevels = new List<string>();
        unlockedItems = new List<string>();
        flags = new Dictionary<string, bool>();
        masterVolume = 1f;
        musicVolume = 0.8f;
        sfxVolume = 0.9f;
        graphicsQuality = 2;
    }
}
```

## Performance Optimization Patterns

### 1. Object Pooling with ScriptableObjects
```csharp
[CreateAssetMenu(fileName = "ObjectPool", menuName = "SOAP/Object Pool")]
public class ObjectPool : ScriptableObject
{
    public GameObject prefab;
    public int initialSize = 10;
    public int maxSize = 100;
    
    private Queue<GameObject> pool = new Queue<GameObject>();
    private List<GameObject> activeObjects = new List<GameObject>();
    
    public void Initialize()
    {
        for (int i = 0; i < initialSize; i++)
        {
            GameObject obj = Instantiate(prefab);
            obj.SetActive(false);
            pool.Enqueue(obj);
        }
    }
    
    public GameObject GetObject()
    {
        GameObject obj;
        
        if (pool.Count > 0)
        {
            obj = pool.Dequeue();
        }
        else if (activeObjects.Count < maxSize)
        {
            obj = Instantiate(prefab);
        }
        else
        {
            return null; // Pool exhausted
        }
        
        obj.SetActive(true);
        activeObjects.Add(obj);
        return obj;
    }
    
    public void ReturnObject(GameObject obj)
    {
        if (activeObjects.Contains(obj))
        {
            activeObjects.Remove(obj);
            obj.SetActive(false);
            pool.Enqueue(obj);
        }
    }
    
    public void ReturnAllObjects()
    {
        foreach (var obj in activeObjects.ToArray())
        {
            ReturnObject(obj);
        }
    }
}
```

### 2. Lazy Loading Pattern
```csharp
[CreateAssetMenu(fileName = "LazyLoadData", menuName = "SOAP/Lazy Load Data")]
public class LazyLoadData : ScriptableObject
{
    [SerializeField] private string dataPath;
    [SerializeField] private bool loadOnAwake = false;
    
    [System.NonSerialized] private bool isLoaded = false;
    [System.NonSerialized] private object loadedData;
    
    private void OnEnable()
    {
        if (loadOnAwake)
        {
            LoadData();
        }
    }
    
    public T GetData<T>() where T : class
    {
        if (!isLoaded)
        {
            LoadData();
        }
        
        return loadedData as T;
    }
    
    private void LoadData()
    {
        if (string.IsNullOrEmpty(dataPath))
        {
            Debug.LogWarning("Data path not set!");
            return;
        }
        
        // Load data based on file extension
        if (dataPath.EndsWith(".json"))
        {
            string jsonData = Resources.Load<TextAsset>(dataPath).text;
            loadedData = JsonUtility.FromJson(jsonData, typeof(T));
        }
        else if (dataPath.EndsWith(".asset"))
        {
            loadedData = Resources.Load(dataPath);
        }
        
        isLoaded = true;
    }
    
    public void UnloadData()
    {
        if (loadedData is UnityEngine.Object obj)
        {
            Resources.UnloadAsset(obj);
        }
        
        loadedData = null;
        isLoaded = false;
    }
}
```

## Best Practices

### 1. Data Organization
- Group related data in logical ScriptableObject classes
- Use clear naming conventions
- Provide validation for data integrity
- Include documentation for complex data structures

### 2. Performance Considerations
- Avoid heavy computations in OnEnable
- Use lazy loading for large datasets
- Implement object pooling for frequently created objects
- Profile memory usage regularly

### 3. Maintainability
- Keep ScriptableObjects focused on single responsibilities
- Use inheritance for common functionality
- Provide clear interfaces for data access
- Include comprehensive error handling

### 4. Serialization
- Mark non-serialized fields with [System.NonSerialized]
- Use proper serialization attributes
- Test save/load functionality thoroughly
- Consider version compatibility for save files

---

*SOAP Usage Patterns*
*Version: 1.0.0*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
