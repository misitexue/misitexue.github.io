layout: page
title: "PAGE TITLE"
permalink: /EventSystem.md/

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
