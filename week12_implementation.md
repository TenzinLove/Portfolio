# Implementation

****



## Enhancement in Application

I recently implemented a significant enhancement to the UndacBlue application by introducing a dedicated page called `SecurityAlertsPage`. This page is designed to provide a clear and organized view of security alerts, sorted by their creation date. By organizing alerts based on creation date, users can quickly access the most relevant and recent information.

The seamless navigation from the main `AlertsPage` to the `SecurityAlertsPage` streamlines the transition between creating new alerts and monitoring the history of security alerts. The addition of a distinctive sound upon creating alerts enhances the interactive aspect of the application, providing audible feedback to users to confirm the success of their actions.

### Key Features:

- **Sorting by Creation Date:** Alerts are organized to allow users to easily identify the most recent information.
- **Intuitive Navigation:** The `SecurityAlertsPage` is easily accessible from the main `AlertsPage`, simplifying the user's transition between creating alerts and reviewing the history of security alerts.
- **Auditory Feedback:** To improve the user experience, I added a distinctive sound that is emitted when creating an alert. This provides audible feedback to confirm the success of the user's action.


<br><br>


The different code sections below:

```

   ///last week code...

private async void OnAddAlertClicked(object sender, EventArgs e)
    {
        string alertName = AlertNameEntry.Text;
        if (!string.IsNullOrEmpty(alertName))
        {
            await Database.InsertAlertAsync(alertName);
            LoadAlerts();
            AlertNameEntry.Text = string.Empty; 
        }

        try
        {
            SystemSounds.Exclamation.Play(); 
        }
        catch (Exception ex)
        {
            // Gérer toute exception, par exemple, si le son n'est pas disponible
            Console.WriteLine($"Erreur lors de la lecture du son : {ex.Message}");
        }
    }

    ///code...


    private async void GoToSecurityAlertsPageClicked(object sender, EventArgs e)
    {
        await Navigation.PushAsync(new SecurityAlertsPage());
    }

```


The `try-catch` block was utilized in the code to appropriately handle any exception that might occur during the attempt to play a sound using `SystemSounds.Exclamation.Play()`. This approach was adopted with a focus on robustness and an optimal user experience.

By wrapping the sound playback attempt within a try block, the code ensures that any potential errors are handled in a controlled manner. If an exception occurs during the sound playback, the program will not crash; instead, control will be transferred to the catch block. 
Inside this block, an informative error message is displayed in the console, indicating that there was an error during the sound playback, and the specific error message from the exception is also included.

<br>


I also created the function GoToSecurityAlertsPageClicked that opens the SecurityAlertsPage. In XAML, this is represented by the following code:

```
<Button Text="Go to Security Alerts Page" Clicked="GoToSecurityAlertsPageClicked" />
```

<br> <br>

This is my SecurityAlertsPAge.xaml.cs :

```

using System.Collections.ObjectModel;
using UndacBlue.Data;
using UndacBlue.Models;

namespace UndacBlue.Views;

public partial class SecurityAlertsPage : ContentPage
{
    private ObservableCollection<Alert> SecurityAlerts { get; set; }
    private Database Database { get; set; }

    public SecurityAlertsPage()
    {
        InitializeComponent();
        Database = new Database();
        SecurityAlerts = new ObservableCollection<Alert>();
        SecurityAlertsListView.ItemsSource = SecurityAlerts;

        LoadSecurityAlerts();
    }

    private async void LoadSecurityAlerts()
    {
        SecurityAlerts.Clear();
        var alerts = await Database.GetAlertsAsync();
        foreach (var alert in alerts.OrderBy(a => a.Timestamp))
        {
            SecurityAlerts.Add(alert);
        }
    }
}

```


The code is understandable, I display the alerts and I used foreach and OrderBy to organize all alerts by their creation date.

<br>

The SecurityAlertsPage.xaml :

```

<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="UndacBlue.Views.SecurityAlertsPage"
             xmlns:local="clr-namespace:UndacBlue"
             Title="SecurityAlertsPage">
    <StackLayout>
        <Label Text="Security Alerts Page" FontSize="Title" HorizontalOptions="CenterAndExpand" VerticalOptions="CenterAndExpand" />

        <ListView x:Name="SecurityAlertsListView" ItemsSource="{Binding SecurityAlerts}" HasUnevenRows="True">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <StackLayout Orientation="Horizontal" Padding="10">
                            <Label Text="{Binding Name}" FontSize="18" />
                            <Label Text="{Binding Timestamp, StringFormat='{0:dd/MM/yyyy HH:mm:ss}'}" FontSize="13" />
                        </StackLayout>
                    </ViewCell>
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>


    </StackLayout>
</ContentPage>

```

<br>

This XAML code defines how the `ListView` named `SecurityAlertsListView` should display items from the `SecurityAlerts` collection on the `SecurityAlertsPage` page.

+ The property `HasUnevenRows="True"` allows for variable row heights based on the content
+ A horizontal `StackLayout` is used to visually organize elements within each cell, with a margin of 10 pixels
+ `<Label Text="{Binding Name}" FontSize="18" />` is a label that displays the `Name` property of the bound object. Each item in the list will have a label showing the alert name
+ `<Label Text="{Binding Timestamp, StringFormat='{0:dd/MM/yyyy HH:mm:ss}'}" FontSize="13" />` is another label that displays the `Timestamp` property of the bound object, formatted as day, month, year, hour, minute, and second

****

<br><br>


I unfortunately encountered a major obstacle in the testing process of my code, a situation I shared with my colleagues over the weekend. The error message that presented itself is as follows:

Severity Code Description Project File Line Status
Error CS0017 Multiple entry points defined in the program. Compile with /main option to specify the type that contains the entry point. UndacBlue (net6.0-android) C:\Users\Math R\Source\Repos\AloiSan\UndacBlue\PersonnelRequestManager.cs 6 Active

This error, regrettably unfamiliar to me, requires thorough investigation to understand its source. My team and I are working to resolve this issue and appreciate your understanding during this troubleshooting phase. Our goal is to address this situation promptly, resume testing, and contribute fully to the project's progress.

