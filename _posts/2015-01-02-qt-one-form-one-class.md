---
layout: post
title: "[Qt]为每一个ui文件生成相应的类"
description: ""
category: coding
tags: [qt]
---
{% include JB/setup %}

对于引用到project中的ui文件，Qt通过User Interface Compiler (uic)进行识别，并且编译生成相应的`ui_filename.h`头文件。

通过单继承的方式可以为对每个UI文件生成对应的类，该子类继承自窗体类，并且根据引用的UI文件生成成员变量。

<!--more-->

例如，存在两个UI文件分别问`oldform.ui` 和 `newform.ui`,就构造两个相应的

**newform.cpp**

```
#include "newform.h"
#include "ui_newform.h"

newform::newform(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::newform)
{
    ui->setupUi(this);
}

newform::~newform()
{
    delete ui;
}

```


**oldform.cpp**

```
#include "oldform.h"
#include "ui_oldform.h"

oldform::oldform(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::oldform)
{
    ui->setupUi(this);
    ui->buttonBox->button(QDialogButtonBox::Ok)->setEnabled(false);
}

oldform::~oldform()
{
    delete ui;
}

```

由于UI类定义在`namespace Ui`下


```
namespace Ui {
class newform;
}
```


，故需要` ui(new Ui::newform)`进行初始化。

在子类内部通过ui对象访问ui设计文件中的控件

```
 ui->buttonBox->button(QDialogButtonBox::Ok)->setEnabled(false);
```

