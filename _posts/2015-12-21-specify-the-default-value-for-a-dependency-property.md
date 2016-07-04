---
layout:     post
title:      Specify the default value for a dependency property
date:       2015-12-21
summary:    When working with UserControls on Xamarin Forms / WPF, values of the control should be bindable by the consumer. Here's a quick example of this in action and how to specify a default value if the consumer does not bind to the property.  
categories: xamarin xaml wpf user-control fundamentals
---

When working with UserControls on Xamarin Forms / WPF, values of the control should be bindable by the consumer. Here's a quick example of this in action and how to specify a default value if the consumer does not bind to the property.

    public LoadingView : UserControl
    {

        public static readonly DependencyProperty LoadingTextProperty = DependencyProperty.Register("LoadingText",
            typeof (string), typeof (LoadingView), new PropertyMetadata("Loading", null));


        public string Title
        {
            get { return GetValue(LoadingText).ToString(); }
            set { SetValue(LoadingText, value); }
        }

    }

In the above sample you will see that a default value is passed into the constructor of `PropertyMetadata`. If a client does not bind/specify a value then `Loading` will be default value. For more information see MSDN - [PropertyMetadata Constructor](https://msdn.microsoft.com/en-us/library/ms557329(v=vs.110).aspx).

