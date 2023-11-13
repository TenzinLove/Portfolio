# Project work 2



At the beginning of our courses, I must admit that the C# language was entirely foreign to me.
With no prior experience, every new concept posed a challenge for me. However, I tried to adapt, 
making an effort to grasp the fundamental concepts of the language.

Despite my efforts, I currently find myself faced with a task that far exceeds my current skills. 
The task, "As an UNDAC Team Leader, I want to view an overall status map of the area so that I can react to changing events,"
seems to be too hard. 

I found several separate codes that show:

+ Showing the Map:

```

\\\xaml

<ContentPage ...
             xmlns:maps="clr-namespace:Microsoft.Maui.Controls.Maps;assembly=Microsoft.Maui.Controls.Maps">
    <maps:Map x:Name="map" />
</ContentPage>



\\\xaml.cs

using Map = Microsoft.Maui.Controls.Maps.Map;

namespace WorkingWithMaps
{
    public class MapTypesPageCode : ContentPage
    {
        public MapTypesPageCode()
        {
            Map map = new Map();
            Content = map;
        }
    }
}

````

 <br> 

 + Showing a Specific Location:
 


 ```

 using Microsoft.Maui.Maps;
using Map = Microsoft.Maui.Controls.Maps.Map;
...

Location location = new Location(36.9628066, -122.0194722);
MapSpan mapSpan = new MapSpan(location, 0.01, 0.01);
Map map = new Map(mapSpan);

```

<br>


+ Mooving the map:

```
using Microsoft.Maui.Maps;
using Microsoft.Maui.Controls.Maps.Map;
...

MapSpan mapSpan = MapSpan.FromCenterAndRadius(location, Distance.FromKilometers(0.444));
map.MoveToRegion(mapSpan);

```

<br>


+ Zooming the map:

```
double zoomLevel = 0.5;
double latlongDegrees = 360 / (Math.Pow(2, zoomLevel));
if (map.VisibleRegion != null)
{
    map.MoveToRegion(new MapSpan(map.VisibleRegion.Center, latlongDegrees, latlongDegrees));
}

```


I  have several pieces of information, but for the task, I always encounter one 
difficulty or another. I hope to be able to finish quickly.


In an attempt to progress, I tried to correct my teammates' codes using various online tools. 
Unfortunately, this approach proved ineffective, as I couldn't fully grasp the logic behind these solutions. 
As a result, I find myself unable to make a meaningful contribution to the team's progress.

I am aware of my current limitations, but I remain determined to learn. 

*****

Moreover, I reworked on my last code because there was an issue with the transcription of data into the database.

The problematic part of the code is:

```


    internal static async Task RaiseAlert(string message, string sender, string recipient)
        {
            var alert = new Alert
            {
                Message = message,
                Sender = sender,
                Recipient = recipient,
                Timestamp = DateTime.Now 
            };

            await Database.InsertAsync(alert); 
        }

```

I noticed that when clicking, nothing was happening in the database, and that my function was simply incorrect.
Additionally, I suppose that the asynchronous method is not serving me. So, I modified the code as follows:

```

internal static Task RaiseAlert(string message, string sender, string recipient)
        {
            var alert = new Alert
            {
                Message = message,
                Sender = sender,
                Recipient = recipient,
                Timestamp = DateTime.Now 
            };

             connection.Insert(alert); 
        }


```