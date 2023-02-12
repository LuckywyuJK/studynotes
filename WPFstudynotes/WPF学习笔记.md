# WPF学习笔记(窗体和常用容器的使用)
[TOC]

## 窗体(Window)

### 常用属性：

- WindowStyle 窗口的边框样式 
- WindowStartupLocation 第一次启动出现的位置 一般主窗体设置成“CenterSceen"   中心显示
- SizeToContent  设置根据内容调整大小
- AllowsTransparency  设置窗体是否透明

###  圆角无边框窗体设置及效果展示

```c#
//Window属性设置
 WindowStyle="None" AllowsTransparency="True" Background="Transparent">
 //在window里面用Border容器包裹，属性设置如下
    <Border Margin="5" Background="#EEE" CornerRadius="5" MouseLeftButtonDown="Border_MouseLeftButtonDown">
        <Border.Effect>
            <DropShadowEffect ShadowDepth="0" Color="Gray" Direction="0" Opacity="0.3" BlurRadius="10"/>
        </Border.Effect>
    </Border>
```

效果展示：

![image-20230211222505744](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/WPFstudynotes/image-20230211222505744.png)

## Grid

> 网格式布局模式

### 基本属性：

- ColumnDefinitions  列定义；该属性里面几个ColumnDefinition容器就被分几列

- RowDefinitions  行定义； 该属性里面有几个RowDefinition容器就被分割为几行

### 附加属性：

- Grid.Row   定义该控件在Grid容器具体在第几行(默认第0行)

- Grid.Column  定义该控件在Grid容器具体在第几列(默认第0列)

### 代码及效果展示

```C#
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

![image-20230212202959975](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/WPFstudynotes/image-20230212202959975.png)

## StackPanel

> 垂直或水平入栈方式排列

### 基本属性:

Orientation：设置排列方向；水平排列或者垂直排列

### 代码及效果展示

```c#
//设置成水平列    
<StackPanel Orientation="Horizontal">
        <Button Content="按钮1"/>
        <Button Content="按钮2"/>
        <Button Content="按钮3"/>
        <Button Content="按钮4"/>
    </StackPanel>
```

效果展示：![image-20230212204708084](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/WPFstudynotes/image-20230212204708084.png)

```c#
//设置成垂直方向排列    
<StackPanel Orientation="Vertical" >
        <Button Content="按钮1"/>
        <Button Content="按钮2"/>
        <Button Content="按钮3"/>
        <Button Content="按钮4"/>
    </StackPanel>
```

效果展示：![image-20230212205024222](https://cdn.jsdelivr.net/gh/LuckywyuJK/studynotes@master/WPFstudynotes/image-20230212205024222.png)

## Border

> 装饰性控件