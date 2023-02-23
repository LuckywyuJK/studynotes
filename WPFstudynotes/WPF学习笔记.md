# WPF学习笔记(基础功能使用)
[TOC]

## 窗体(Window)

### 常用属性：

- WindowStyle 窗口的边框样式 
- WindowStartupLocation 第一次启动出现的位置 一般主窗体设置成“CenterSceen"   中心显示
- SizeToContent  设置根据内容调整大小
- AllowsTransparency  设置窗体是否透明

###  圆角无边框窗体设置及效果展示

```xaml
<!--Window属性设置-->
<Window>WindowStyle="None" AllowsTransparency="True" Background="Transparent"></Window>
 <!--在window里面用Border容器包裹，属性设置如下-->
    <Border Margin="5" Background="#EEE" CornerRadius="5" MouseLeftButtonDown="Border_MouseLeftButtonDown">
        <Border.Effect>
            <DropShadowEffect ShadowDepth="0" Color="Gray" Direction="0" Opacity="0.3" BlurRadius="10"/>
        </Border.Effect>
    </Border>
```

效果展示：

![image-20230211222505744](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/studynotes_pirture/image-20230211222505744.png)

## 布局控件

1. Grid
2. StackPanel
3. DockPanel
4. WrapPanel
5. UniformGrid
6. Canvas
7. InkCanvas
8. Border（装饰控件：背景色/边框 圆角 子对象也只能一个)

### Grid

> 网格式布局模式

#### 基本属性：

- ColumnDefinitions  列定义；该属性里面几个ColumnDefinition容器就被分几列

- RowDefinitions  行定义； 该属性里面有几个RowDefinition容器就被分割为几行

#### 附加属性：

- Grid.Row   定义该控件在Grid容器具体在第几行(默认第0行)

- Grid.Column  定义该控件在Grid容器具体在第几列(默认第0列)

#### 代码及效果展示

```xaml
 <Grid>
        <Grid.RowDefinitions>
            <RowDefinition/>
            <RowDefinition/>
            <RowDefinition/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition/>
            <ColumnDefinition/>
            <ColumnDefinition/>
        </Grid.ColumnDefinitions>
        <Button Content="默认第0行第0列"/>
        <Button Content="第3行第3列" Grid.Row="3" Grid.Column="3"/>
    </Grid>
```

效果展示：

![image-20230212202959975](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/studynotes_pirture/image-20230212202959975.png)

### StackPanel

> 垂直或水平入栈方式排列

#### 基本属性:

Orientation：设置排列方向；水平排列或者垂直排列

#### 代码及效果展示

```xaml
<!--设置成水平列-->    
<StackPanel Orientation="Horizontal">
        <Button Content="按钮1"/>
        <Button Content="按钮2"/>
        <Button Content="按钮3"/>
        <Button Content="按钮4"/>
    </StackPanel>
```

效果展示：![image-20230212204708084](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/studynotes_pirture/image-20230212204708084.png)

```xaml
<!--设置成垂直方向排列-->    
<StackPanel Orientation="Vertical" >
        <Button Content="按钮1"/>
        <Button Content="按钮2"/>
        <Button Content="按钮3"/>
        <Button Content="按钮4"/>
    </StackPanel>
```

效果展示：![image-20230212205024222](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/studynotes_pirture/image-20230212205024222.png)

### Border

> 装饰性控件



### 自定义容器

> 所有容器都继承至Panel; 容器绘制主要重写MeasureCore和ArrangeOverride两个方法

- 重写MeasureCore方法测量子元素所需大小

- 重写ArrangeOverride方法给子元素进行排列

## 资源管理

- 文件资源(图像，音频等)
```xaml
<!--文件资源调用的几种形式-->
<!--图片资源的调用-->
<Image Source="pack://application:,,,/WPFCodeText;component/Assets/Docker.png"/>
<!--字体资源的调用-->
<TextBlock Text="&#xe60d;" FontFamily="WPFCodeText;component/Assets/#iconfont" FontSize="50" Foreground="OrangeRed"/>
<TextBlock Text="&#xe60b;" FontFamily="/Assets/#iconfont" FontSize="50" Foreground="Green"/>
```
- 对象资源(创建实例化无参构造方法的类)

```xaml
<DockPanel.Resources>
    <sys:Double x:Key="value">100</sys:Double>
</DockPanel.Resources>
```

- 资源字典(ResourceDictionary)的使用

对多个资源进行封装，方便统一管理

资源字典的xaml文件属性中生成操作一般是页

![image-20230218232627995](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/studynotes_pirture/image-20230218232627995.png)

```xaml
<!--新建一个资源字典文件-->
<!--资源字典对象ResourceDictionnary-->
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    xmlns:sys ="clr-namespace:System;assembly=System.Runtime">
    <sys:Double x:Key="value">100</sys:Double>
</ResourceDictionary>
<!--在窗体中调用-->
<Window x:Class="WPFCodeText.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WPFCodeText"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Window.Resources>
        <!--窗体调用资源字典文件-->
        <ResourceDictionary Source="/Res.xaml"/>
    </Window.Resources>
    <!--此处使用的静态资源使用StaticResource关键字；动态资源使用DynamicResuorce-->
        <Button Background="Beige" Height="{StaticResource value}"/>
    </DockPanel>
</Window>
```



##  样式(Style)管理

> 可以对控件的属性进行统一的管理

Style基本属性

- Settter.Property 属性参数设置
- Style.Resource   样式资源
- Style.Triggers   样式触发器

样式练习：

```xaml
<!--结合资源字典将样式封装在字典已被使用-->
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Style x:Key="BorderStyle" TargetType="Border">
        <Setter Property="Background" Value="Orange"/>
        <Setter Property="Width" Value ="100"/>
        <Setter Property="Height" Value ="100"/>
        <Setter Property="CornerRadius" Value ="20"/>
    </Style>
    <Style x:Key="ButtonStyle" TargetType="Button">
        <Setter Property="Width" Value ="100"/>
        <Setter Property="Height" Value ="40"/>
        <Setter Property="Content" Value="请点击我！"/>
        <EventSetter/>
        <Style.Resources/>
        <!--样式触发器-->
        <Style.Triggers>
            <!--Button事件中鼠标点击和鼠标经过时触发的字体变化效果-->
            <!--若下方触发器顺序，将鼠标经过的触发器写前面；会导致点击鼠标样式无法效果-->
            <!--主要2个样式同时触发作用到同一属性中，由于代码执行顺序，后写的触发器效果会覆盖前者-->
            <!--<Trigger Property="IsMouseOver" Value="True">
                <Setter Property="Foreground" Value="Orange"/>
            </Trigger>
            <Trigger Property="IsMouseCaptured" Value="True">
                <Setter Property="Foreground" Value="Green"/>
            </Trigger>-->
            <!--多个条件同时触发的效果-->
            <MultiTrigger>
                <MultiTrigger.Conditions>
                    <Condition Property="IsMouseOver" Value="True"/>
                    <Condition Property="IsMouseCaptured" Value="True"/>
                </MultiTrigger.Conditions>
                <MultiTrigger.Setters>
                    <Setter Property="Foreground" Value="Red"/>
                </MultiTrigger.Setters>
            </MultiTrigger>
        </Style.Triggers>
    </Style>
</ResourceDictionary>
```

在给Border和Button设置样式属性

```xaml
<Window x:Class="WY.WPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WY.WPF"
        mc:Ignorable="d"
        Title="WPF练习" Height="450" Width="800"
        FontWeight="Black" WindowStartupLocation="CenterScreen">
    <!--资源指向-->
    <Window.Resources>
        <ResourceDictionary Source="pack://application:,,,/WY.WPF;component/ResDictionary.xaml"/>
    </Window.Resources>
    <StackPanel>
        <Image Source="pack://application:,,,/WY.WPF;component/Asstes/Docker.png" Height="50" HorizontalAlignment="Left"/>
        <TextBlock Text="&#xe60b;" FontFamily="pack://application:,,,/WY.WPF;component/Asstes/#iconfont" FontSize="50"/>
        <Border Style="{StaticResource BorderStyle}" Margin="10"/>
        <Button Style="{StaticResource ButtonStyle}" HorizontalAlignment="Left"/>
    </StackPanel>
</Window>
```

## 模板

- 控件模板 ControlTemplate
- 数据模板 DataCtroTemplate
- 模板选择器

## 依赖属性(DependencyProperty)

- 声明     依赖属性必须注册在依赖对象中声明（继承DependencyObject）
- 注册(静态构造方法)  通过new PropertyMetadata给依赖属性一个默认值
- 包装

```c#
    public partial class MainWindow : Window
    {
        //第一步:声明依赖属性
        //依赖属性必须注册在依赖对象中（继承DependencyObject）
        public static readonly DependencyProperty VlueProperty;
        //第二步：注册
        static MainWindow()
        {
            VlueProperty = DependencyProperty.Register("VlueProperty", typeof(double),typeof(MainWindow));
        }
        public MainWindow()
        {
            InitializeComponent();
        }
        //第三步：属性包装
        public double Vlue
        {
            get { return (double)this.GetValue(VlueProperty); }
            set { this.SetValue(VlueProperty,1.0); }
        }

    }
```

