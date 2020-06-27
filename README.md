# Unity Ad Manager
A quick, easy and reusable AdManager solution for Unity Ads

For a full explination of this class and step-by-step creation instructions, find the full video on our YouTube channel here => https://youtube.com/comp3interactive

### Setup
- Add the AdManager.cs file to your project
- Open the AdManager.cs file and change the storeID variables and video ID variables to match your own which can be found on the Unity Dashboard > Project > Monetization > Placements
```csharp
private static readonly string storeID = "???????";
private static readonly string videoID = "video";
private static readonly string rewardedID = "rewardedVideo";
private static readonly string bannerID = "bannerAd";
```

### Public methods
```csharp
public static void ShowStandardAd(){...}
```
Calling ShowStandardAd() will display a skippable interstitial ad in screen

```csharp
public static void ShowRewardedAd(Action success, Action skipped, Action failed){...}
```
Calling ShowRewardedAd(Action,Action,Action) will show an un-skippable rewarded ad, the three required Action parameters correspond with Success, Skip and Failure criteria. These are to be passed in when calling the method and will be used as callbacks upon ad completion. Your Skip and Failure methods will more than likely be the same regardless of which rewarded ad is playing but the Success Action can be used to reward the player in multiple ways depending on the desired outcome. Example: 

```csharp
public class AdManagerTester : MonoBehaviour
{
    public void Start()
    {
        // Call ShowRewardedAd using the three required methods to give an extra life
        AdManager.ShowRewardedAd(SuccessLife, Skip, Failed); 
        
        // Call ShowRewardedAd using the three required methods to give extra coins
        AdManager.ShowRewardedAd(SuccessCoins, Skip, Failed); 
    }
    
    // What happens if the rewarded ad is watched successfully
    void SuccessLife()
    {
        Debug.Log("Ad watched - +1 life");
    }
    void SuccessCoins()
    {
        Debug.Log("Ad watched - 100 coins");
    }
    
    // What happens if the rewarded ad is skipped
    void Skip()
    {
        Debug.Log("Ad skipped");
    }
    
    // What happens if the rewarded ad fails to load
    void Failed()
    {
        Debug.Log("Ad failed to load");
    }
}
```

```csharp
public static void ShowBanner(){...}
```
Calling ShowBannerAd() will display a banner ad at the BOTTOM_CENTER of the mobile screen by default, this positioning can be altered in AdManager.cs (ShowBannerWhenReady()).
Possible banner ad positionings are:
```csharp
BannerPosition.TOP_LEFT
BannerPosition.TOP_CENTER
BannerPosition.TOP_RIGHT
BannerPosition.CENTER
BannerPosition.BOTTOM_LEFT
BannerPosition.BOTTOM_CENTER
BannerPosition.BOTTOM_RIGHT
```

```csharp
public static void HideBanner(){...}
```
Calling HideBanner() will hide any visible banner ad on screen
