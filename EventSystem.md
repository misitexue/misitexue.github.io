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
public class GameManager : MonoBehaviour
{
    [SerializeField] private VoidEventChannelSO _exitGame = default;      // 跟踪游戏状态
    
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