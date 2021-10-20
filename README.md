# Websites-on-C-Sharp





## **Better website plugins than Internet Explorer og Windows webBrowser**

- [CefSharp](https://www.nuget.org/packages/CefSharp.WinForms/)



## **How to make WinForm look like website?**

- [EasyTabs](https://www.nuget.org/packages/EasyTabs/)


### ***--------Code--------***

- First Change Form1 name to Appcontainer

```
using System;
using EasyTabs;

namespace YOUR_NAME_SPACE
{
    public partial class Appcontainer : TitleBarTabs
    {
        public Appcontainer()
        {
            InitializeComponent();

            AeroPeekEnabled = true;
            TabRenderer = new ChromeTabRenderer(this);
        }

        public override TitleBarTab CreateTab()
        {
            return new TitleBarTab(this)
            {
                Content = new frmBrowser
                {
                    Text = "Your Browser Name"
                }
            };
        }
    }
}
```
- **Change your program.cs to this**

```
using EasyTabs;
using System;
using System.Windows.Forms;

namespace YOUR_NAME_SPACE
{
    static class Program
    {
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Appcontainer websitec = new Appcontainer();

            websitec.Tabs.Add(
                //djwiajdoij
                new TitleBarTab(websitec)
                {
                    Content = new frmBrowser
                    {
                        Text = "YOUR WEBSITE NAME"
                    }
                }
            );

            websitec.SelectedTabIndex = 0;

            TitleBarTabsApplicationContext applicationContext = new TitleBarTabsApplicationContext();
            applicationContext.Start(websitec);
            Application.Run(applicationContext);

        }
    }
}
```

- **Create New Form named "frmBrowser" and add this code**

```
using EasyTabs;
using Microsoft.Win32;
using System;
using System.Windows.Forms;

namespace YOUR_NAME_SPACE
{
    public partial class frmBrowser : Form
    {
        public frmBrowser()
        {
            InitializeComponent();

            var appName = System.Diagnostics.Process.GetCurrentProcess().ProcessName + ".exe";

            using (var Key = Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Microsoft\Internet Explorer\Main\FeatureControl\FEATURE_BROWSER_EMULATION", true))
                Key.SetValue(appName, 99999, RegistryValueKind.DWord);

            webBrowser2.Navigate("https://google.com");
        }

        protected TitleBarTabs ParentTabs
        {
            get
            {
                return (ParentForm as TitleBarTabs);
            }
        }
    }
}
```
