---
layout: post
title: "[Qt] FindDialog in Qt5"
description: ""
category: coding
tags: [qt]
---
{% include JB/setup %}


使用Qt5环境

qt5中，build出错：
```
error: forward declaration of 'class QCheckBox'  class QCheckBox;
```
头文件引用：

`#include <QtGui>`改为 `#include <QtWidgets>`

生成的对话框没有显示任何的widget

加入`setLayout(mainLayout);`

<!--more-->

__finddia.h__

```
#ifndef FINDDIA_H
#define FINDDIA_H

#include <QDialog>
class QCheckBox;
class QLabel;
class QLineEdit;
class QPushButton;

class FindDia : public QDialog
{
    Q_OBJECT

public:
    FindDia(QWidget *parent = 0);
    ~FindDia();

signals:
   void findNext(const QString &str,Qt::CaseSensitivity cs);
   void findPrevious(const QString &str,Qt::CaseSensitivity cs);

private slots:
   void findClicked();
   void enableFindButton(const QString &text);

private:
   QLabel *label;
   QLineEdit *lineEdit;
   QCheckBox *caseCheckBox;
   QCheckBox *backwardCheckBox;
   QPushButton *findButton;
   QPushButton *closeButton;
};

#endif // FINDDIA_H

```

__finddia.cpp__

```
#include <QtGui>
#include <QtWidgets>
#include "finddia.h"

FindDia::FindDia(QWidget *parent)
    : QDialog(parent)
{
    label = new QLabel(tr("Find &what:"));
    lineEdit = new QLineEdit;
    label->setBuddy(lineEdit);

    caseCheckBox = new QCheckBox(tr("Match &case"));
    backwardCheckBox = new QCheckBox(tr("Search &backward"));

    findButton = new QPushButton(tr("&Find"));
    findButton->setDefault(true);
    findButton->setEnabled(false);

    closeButton = new QPushButton(tr("Close"));

    connect(closeButton,SIGNAL(clicked()),this,SLOT(close()));
    connect(lineEdit,SIGNAL(textChanged(const QString &)),this,SLOT(enableFindButton(const QString &)));
    connect(findButton,SIGNAL(clicked()),this,SLOT(findClicked()));

    QHBoxLayout *topLeftLayout = new QHBoxLayout;
    topLeftLayout->addWidget(lineEdit);
    topLeftLayout->addWidget(label);

    QVBoxLayout *leftLayout = new QVBoxLayout;
    leftLayout->addLayout(topLeftLayout);
    leftLayout->addWidget(caseCheckBox);
    leftLayout->addWidget(backwardCheckBox);


    QVBoxLayout *rightLayout = new QVBoxLayout;
    rightLayout->addWidget(findButton);
    rightLayout->addWidget(closeButton);
    rightLayout->addStretch();


    QHBoxLayout *mainLayout = new QHBoxLayout;
    mainLayout->addLayout(leftLayout);
    mainLayout->addLayout(rightLayout);
    mainLayout->addWidget(findButton);

    setWindowTitle(tr("Find"));
    setLayout(mainLayout);
    setFixedHeight(sizeHint().height());

}

void FindDia::findClicked(){

    QString text = lineEdit->text();
    Qt::CaseSensitivity cs = caseCheckBox->isChecked() ? Qt::CaseSensitive : Qt::CaseInsensitive;
    if (backwardCheckBox->isChecked()){
        emit findPrevious(text,cs);
    }
    else {
        emit findNext(text,cs);
    }

}

void FindDia::enableFindButton(const QString &text){

    findButton->setEnabled(!text.isEmpty());
}

FindDia::~FindDia()
{

}
```

__main.cpp__

```
#include "finddia.h"
#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    FindDia *w = new FindDia;

    w->show();
    return a.exec();
}
```

