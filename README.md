# EventToBehavior in ListView

The ListView event can be converted into commands using [Behaviors](https://developer.xamarin.com/guides/xamarin-forms/behaviors/). To achieve this, create a command in the ViewModel class and associate it to the ListView event using `Behaviors`.

```
<listView:SfListView x:Name="listView" ItemsSource="{Binding contactsinfo}">
    <listView:SfListView.Behaviors>
        <local:EventToCommandBehavior EventName="SelectionChanged" Command="{Binding SelectionChangedCommand}"/>
    </listView:SfListView.Behaviors>
</listView:SfListView>
```
```
public class ContactsViewModel
{
    public Command<ItemSelectionChangedEventArgs> selectionChangedCommand;

    public Command<ItemSelectionChangedEventArgs> SelectionChangedCommand
    {
        get { return selectionChangedCommand; }
        set { selectionChangedCommand = value; }
    }

    public ContactsViewModel()
    {
        SelectionChangedCommand = new Command<Syncfusion.ListView.XForms.ItemSelectionChangedEventArgs>(OnSelectionChanged);
    }

    private void OnSelectionChanged(ItemSelectionChangedEventArgs obj)
    {
        App.Current.MainPage.DisplayAlert("Alert", (obj.AddedItems[0] as Contacts).ContactName + " is selected", "OK");
    }
}
```

To know more about MVVM in ListView, please refer our documentation [here](https://help.syncfusion.com/xamarin/sflistview/mvvm).
