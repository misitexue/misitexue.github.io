# 系统架构&源码展示

### 事件系统架构

![Image](EventSystem.jpg)
![Image](EventSystem2.jpg)

### 源码

```C#
[CreateAssetMenu(menuName = "Events/Void Event Channel")]
public class VoidEventChannelSO : ScriptableObject
{
    public UnityAction OnEventRaised;
    
    public void RaiseEvent()
    {
        if (OnEventRaised != null)
            OnEventRaised.Invoke();
    }      
}

```

```C#
public class UIManager : MonoBehaviour
{
    [SerializeField] private VoidEventChannelSO _exitGame = default;
	
    public void ClickExitGame()
    {
        _exitGame.RaiseEvent();
    }
}
```

```C#
public class GameManager : MonoBehaviour
{
    [SerializeField] private VoidEventChannelSO _exitGame = default;
    
    private void OnEnable()
    {
        _exitGame.OnEventRaised += ExitGame;
    }
    
    private void OnDisable()
    {
        _exitGame.OnEventRaised -= ExitGame;
    }
	
    private void ExitGame()
    {
        debug.log("Exit Game!")
    }
}
```
