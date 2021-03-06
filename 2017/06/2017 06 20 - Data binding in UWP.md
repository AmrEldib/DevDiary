# Data binding in UWP

Notes while reading [Data binding in Depth](https://docs.microsoft.com/en-us/windows/uwp/data-binding/data-binding-in-depth)

Use [{x:Bind}](https://docs.microsoft.com/en-us/windows/uwp/xaml-platform/x-bind-markup-extension) or [{Binding}](https://docs.microsoft.com/en-us/windows/uwp/xaml-platform/binding-markup-extension).  
{x:Bind} is new for Windows 10 and it has better performance. However, {Binding} has more features. Here's a [comparison](https://docs.microsoft.com/en-us/windows/uwp/data-binding/data-binding-in-depth#xbind-and-binding-feature-comparison).  

Every binding involves these pieces:  
- _Binding source_: the class containing the data
- _Binding target_: the UI displaying the data
- _Binding object_: the connection between the two. It's generated by XAML automatically.  

You can Base your class on [BindableBase](https://github.com/Microsoft/Windows-appsample-networkhelper/blob/master/DemoApps/QuizGame/Common/BindableBase.cs) as a quick way to implement [INotifyPropertyChanged](https://msdn.microsoft.com/library/windows/apps/xaml/system.componentmodel.inotifypropertychanged.aspx).  
BindableBase isn't part of the .NET standard library, it's a commonly used custom class.  

Here's how to the binding source can handle common binding scenarios:  
- __Bind to an object__: Can be any object
- __Get property change updates from a bound object__: Object must implement System.ComponentModel. INotifyPropertyChanged.
- __Bind to a collection.__: List(Of T)
- __Get collection change updates from a bound collection__: ObservableCollection(Of T)
- __Implement a collection that supports binding__: Extend List(Of T) or implement IList, IList(Of Object), IEnumerable, or IEnumerable(Of Object). Binding to generic IList(Of T) and IEnumerable(Of T) is not supported.
- __Implement a collection that supports collection change updates__: Extend ObservableCollection(Of T) or implement (non-generic) IList and INotifyCollectionChanged.
- __Implement a collection that supports incremental loading__: Extend ObservableCollection(Of T) or implement (non-generic) IList and INotifyCollectionChanged. Additionally, implement ISupportIncrementalLoading.

