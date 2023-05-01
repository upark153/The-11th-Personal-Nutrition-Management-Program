# The-11th-Personal-Nutrition-Management-Program
You can register, edit, add, or delete nutritional supplements. Programmed in c++ qt.
![image](https://user-images.githubusercontent.com/115389450/235425186-d87494c6-7fb2-4bec-b12e-2175c1e3ce7f.png)
![image](https://user-images.githubusercontent.com/115389450/235425221-1fc8f55b-b19c-4649-ab1f-c5d7dd3d3f4b.png)
![image](https://user-images.githubusercontent.com/115389450/235425260-f1502e42-a897-43e9-8054-92d4ea862827.png)
![image](https://user-images.githubusercontent.com/115389450/235425307-788de2e3-bead-4ebd-b484-d1eff56b307a.png)
![image](https://user-images.githubusercontent.com/115389450/235425332-669e546c-173a-48c9-97a5-2c02756b59b2.png)
![image](https://user-images.githubusercontent.com/115389450/235425377-b8e32d4e-d013-4350-bd7d-52d8ff563a1b.png)
![image](https://user-images.githubusercontent.com/115389450/235425414-4984f080-ecd9-44ae-a96f-72c8ea7451ff.png)
![image](https://user-images.githubusercontent.com/115389450/235425484-c3ac6f66-d252-4c8f-b73e-ae9c37b60e9e.png)
![image](https://user-images.githubusercontent.com/115389450/235425528-d9329c60-1574-4ed7-974b-f136ed9f880a.png)
![image](https://user-images.githubusercontent.com/115389450/235425564-192c4427-9554-4d93-9bc5-80c1b682b98f.png)
![image](https://user-images.githubusercontent.com/115389450/235425606-5b07ebc9-fc41-448e-9b7a-f9a2abe6807b.png)
![image](https://user-images.githubusercontent.com/115389450/235425635-5a4b9de5-1b80-4402-9666-0228144d2572.png)
![image](https://user-images.githubusercontent.com/115389450/235425674-f0313be8-f693-4f2b-a55f-d5037a8d11ca.png)
![image](https://user-images.githubusercontent.com/115389450/235425700-76e2bf0e-8f47-472c-8ac5-6b69ce8d00c2.png)
![image](https://user-images.githubusercontent.com/115389450/235425738-1aa0bd7b-78ee-45b3-8c01-7ad5ca754cca.png)
![image](https://user-images.githubusercontent.com/115389450/235425829-ed359324-6a38-423b-b714-5fe2c62f994f.png)
![image](https://user-images.githubusercontent.com/115389450/235425859-4ad831bc-6717-4560-b3d8-32768e673cf0.png)
![image](https://user-images.githubusercontent.com/115389450/235425917-791e58c0-c02c-4c4d-a380-47d887d51029.png)
![image](https://user-images.githubusercontent.com/115389450/235426026-00a4d64a-3211-443c-8081-dce3b70efc37.png)
```
cmake_minimum_required(VERSION 3.5)

project(ManagementNutritionWithPill VERSION 0.1 LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets)

set(PROJECT_SOURCES // 이 부분이 중요함. 추가된 파일을 여기에 꼭 포함시켜줘야 된다.
        main.cpp
        mainwindow.cpp
        mainwindow.h
        mainwindow.ui
        addvitaminsupplement.h
        addvitaminsupplement.cpp
        addvitaminsupplement.ui
        registernutrionfacts.h
        registernutrionfacts.cpp
        registernutrionfacts.ui
        findvitaminsupplement.h
        findvitaminsupplement.cpp
        findvitaminsupplement.ui
        findnutritionfacts.h
        findnutritionfacts.cpp
        findnutritionfacts.ui
)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_executable(ManagementNutritionWithPill
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
# Define target properties for Android with Qt 6 as:
#    set_property(TARGET ManagementNutritionWithPill APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
#                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
# For more information, see https://doc.qt.io/qt-6/qt-add-executable.html#target-creation
else()
    if(ANDROID)
        add_library(ManagementNutritionWithPill SHARED
            ${PROJECT_SOURCES}
        )
# Define properties for Android with Qt 5 after find_package() calls as:
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
    else()
        add_executable(ManagementNutritionWithPill
            ${PROJECT_SOURCES}
        )
    endif()
endif()

target_link_libraries(ManagementNutritionWithPill PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)

set_target_properties(ManagementNutritionWithPill PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

install(TARGETS ManagementNutritionWithPill
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(ManagementNutritionWithPill)
endif()
```
## 1.1 메인화면 헤더파일 소스코드
```
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow> // 처음 생성할 시 이 코드 한줄만 존재, 이후에 추가한 ui파일 헤더파일을 include 해서 연결한다.
#include "addvitaminsupplement.h"
#include "registernutrionfacts.h"
#include "findvitaminsupplement.h"
#include "findnutritionfacts.h"

QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private slots: // 슬롯을 이용해서 버튼 클릭시 각 ui를 연결시킨다.
    void on_pushButton_clicked();

    void on_pushButton_2_clicked();

    void on_pushButton_3_clicked();

    void on_pushButton_4_clicked();

private:
    Ui::MainWindow *ui; // 중요함. 메인윈도우 헤더파일에 포인터를 이용한 각 ui 주소 설정, 첫단계로 해야할 일이다.
    AddVitaminSupplement *ptrAddVitaminSupplement;
    RegisterNutrionFacts *ptrRegisterNutrionFacts;
    FindVitaminSupplement *ptrFindVitaminSupplement;
    FindNutritionFacts *ptrFindNutritionFacts;
};
#endif // MAINWINDOW_H
```
## 1.1 메인화면 cpp 소스코드
```
#include "mainwindow.h"
#include "./ui_mainwindow.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this); // 2번째 단계, 메인윈도우 c++ 코드에 헤더파일에서 설정한 주소 객체 생성
    // 아래 생성된 객체(ui) 창을 닫을 때 객체가 파괴될 때마다 확인해야 한다. delete를 이용.
    // 아래 생성된 객체를 어떻게 사용할 것인가?
    // 메인 윈도우 ui로 이동하여 확인해보자.
    ptrAddVitaminSupplement = new AddVitaminSupplement();
    ptrRegisterNutrionFacts = new RegisterNutrionFacts();
    ptrFindVitaminSupplement = new FindVitaminSupplement();
    ptrFindNutritionFacts = new FindNutritionFacts();


}

MainWindow::~MainWindow()
{
    // 3번째 단계
    // 창이 닫아질 때, 객체가 파괴될 때 소멸한다
    // 여기에 할당된 모든 메모리가 해제 되지만,
    // 메모리를 모두 지우는 것이 좋다.
    delete ptrAddVitaminSupplement;
    delete ptrRegisterNutrionFacts;
    delete ptrFindVitaminSupplement;
    delete ptrFindNutritionFacts;
    delete ui;
}


void MainWindow::on_pushButton_clicked()
{
    // 4번째 단계
    // 메인 윈도우 ui에서 버튼클릭 시 이동 슬롯 설정.
    // 이렇게 하면 새로운 메서드가 생성이 된 걸 확인할 수 있다.
    ptrAddVitaminSupplement -> show();
}


void MainWindow::on_pushButton_2_clicked()
{
    ptrRegisterNutrionFacts -> show();
}


void MainWindow::on_pushButton_3_clicked()
{
    ptrFindVitaminSupplement -> show();
}


void MainWindow::on_pushButton_4_clicked()
{
    ptrFindNutritionFacts -> show();
}
```
## ﻿1.2 영양제 추가 ui cpp 소스코드
```
#include "addvitaminsupplement.h"
#include "ui_addvitaminsupplement.h"

AddVitaminSupplement::AddVitaminSupplement(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::AddVitaminSupplement)
{
    ui->setupUi(this);
}

AddVitaminSupplement::~AddVitaminSupplement()
{
    delete ui;
}

void AddVitaminSupplement::on_supplement_save_btn_clicked()
{
    QString supplementName = ui -> supplement_name_lineEdit -> text();
    QString supplementType = ui -> supplement_type_lineEdit -> text();
    QString supplementDescription = ui -> supplement_description_textEdit -> toPlainText();
    QString supplementAmount = ui -> Supplement_amount_lineEdit -> text();

    qDebug() << "영양제 이름 : " << supplementName << "영양제 종류 : " << supplementType << "영양제 설명 : " << supplementDescription << "영양제 가격 : " << supplementAmount;
}
```
![image](https://user-images.githubusercontent.com/115389450/235426337-7dddaa7f-19aa-44b8-9ddc-d38d4a9c5fc6.png)
```
#ifndef DATABASEHEADER_H
#define DATABASEHEADER_H

#include <QSqlDatabase> // 그대로 사용하려니 오류가 난다. 해결하자.
#include <QSqlDriver>
#include <QsqlError>
#include <QDebug>
#include <QSqlTableModel>

#endif // DATABASEHEADER_H
```
![image](https://user-images.githubusercontent.com/115389450/235426455-cd674028-2446-47df-9334-c186ee1b142e.png)
```
#include "addvitaminsupplement.h"
#include "ui_addvitaminsupplement.h"

AddVitaminSupplement::AddVitaminSupplement(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::AddVitaminSupplement)
{
    ui->setupUi(this);
}

AddVitaminSupplement::~AddVitaminSupplement()
{
    delete ui;
}

void AddVitaminSupplement::on_supplement_save_btn_clicked()
{
    QString supplementName = ui -> supplement_name_lineEdit -> text();
    QString supplementType = ui -> supplement_type_lineEdit -> text();
    QString supplementDescription = ui -> supplement_description_textEdit -> toPlainText();
    QString supplementAmount = ui -> Supplement_amount_lineEdit -> text();

    qDebug() << "영양제 이름 : " << supplementName << "영양제 종류 : " << supplementType << "영양제 설명 : " << supplementDescription << "영양제 가격 : " << supplementAmount;

    QSqlDatabase database = QSqlDatabase::addDatabase("QMYSQL");
    qDebug() << QSqlDatabase::drivers();
}
```
![image](https://user-images.githubusercontent.com/115389450/235426529-0f64879e-bc66-46f8-a441-64987cda29cf.png)
```
#include "addvitaminsupplement.h"
#include "ui_addvitaminsupplement.h"

AddVitaminSupplement::AddVitaminSupplement(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::AddVitaminSupplement)
{
    ui->setupUi(this);
    qDebug() << QSqlDatabase::drivers();
    db = QSqlDatabase::addDatabase("QMYSQL");
    db.setHostName("127.0.0.1");
    db.setPort(3306);
    db.setDatabaseName("mysupplement");
    db.setUserName("root");
    db.setPassword("0000");
    db.open();

    if (db.open())
    {
        qDebug() << "Database is connected";
    }
    else
    {
        qDebug() << "Database is not connected";
    }
}

AddVitaminSupplement::~AddVitaminSupplement()
{
    delete ui;
}

void AddVitaminSupplement::on_supplement_save_btn_clicked()
{
    QString supplementName = ui -> supplement_name_lineEdit -> text();
    QString supplementType = ui -> supplement_type_lineEdit -> text();
    QString supplementDescription = ui -> supplement_description_textEdit -> toPlainText();
    QString supplementAmount = ui -> Supplement_amount_lineEdit -> text();

    qDebug() << "영양제 이름 : " << supplementName << "영양제 종류 : " << supplementType << "영양제 설명 : " << supplementDescription << "영양제 가격 : " << supplementAmount;

    db.open();
    QSqlDatabase::database().transaction();
    QSqlQuery Query_Insert_Data(db);
    Query_Insert_Data.prepare("INSERT INTO supplement(Name, Type, Description, Amount) VALUES (:Name,:Type,:Description,:Amount)");
    Query_Insert_Data.bindValue(":Name",supplementName);
    Query_Insert_Data.bindValue(":Type",supplementType);
    Query_Insert_Data.bindValue(":Description",supplementDescription);
    Query_Insert_Data.bindValue(":Amount",supplementAmount);
    Query_Insert_Data.exec();
    QSqlDatabase::database().commit();
    db.close();
//    QSqlDatabase db = QSqlDatabase::addDatabase("QMYSQL");
//    db.setHostName("127.0.0.1");
//    db.setPort(3306);
//    db.setDatabaseName("mysupplement");
//    db.setUserName("root");
//    db.setPassword("0000");
//    db.open();

//    QSqlQuery qry;
//    qry.prepare(QString("insert into supplement(Name, Type, Description, Amount) values('%1', '%2', '%3', '%4')")
//                .arg(supplementName).arg(supplementType).arg(supplementDescription).arg(supplementAmount));
//    if(!qry.exec())
//    qDebug() << qry.lastError();

}
```
![image](https://user-images.githubusercontent.com/115389450/235426616-23c7cdd4-6146-4373-8836-68d4722184df.png)
![image](https://user-images.githubusercontent.com/115389450/235426675-ca8387a8-afff-4321-8a73-4f0454935a8b.png)
```
#ifndef DATABASEHEADER_H
#define DATABASEHEADER_H

#include <QSqlDatabase>
#include <QSqlDriver>
#include <QsqlError>
#include <QDebug>
#include <QSqlTableModel>
#include <QSqlQuery>
#include <QSqlQueryModel>
#include <QMessageBox>

class dconnect
{
public:
    QSqlDatabase db; // 데이터베이스 객체 생성

    void connClose()
    {
        db.close();
        db.removeDatabase(QSqlDatabase::defaultConnection);
    }
    bool connOpen()
    {
        db = QSqlDatabase::addDatabase("QMYSQL");
        db.setHostName("127.0.0.1");
        db.setPort(3306);
        db.setDatabaseName("mysupplement");
        db.setUserName("root");
        db.setPassword("0000");
        db.open();
        QSqlDatabase::database().transaction();
        if (db.open())
        {
            qDebug() << "Database is connected";
            return true;
        }
        else
        {
            qDebug() << "Database is not connected";
            return false;
        }
    }
};
#endif // DATABASEHEADER_H
```
###
데이터베이스가 필요한 ui에 include해서 사용하기 위해

따로 데이터베이스 헤더파일에

클래스를 정의하였다.


영양제추가,삭제,수정.h 코드

```
#ifndef ADDVITAMINSUPPLEMENT_H
#define ADDVITAMINSUPPLEMENT_H

#include <QDialog>
#include "databaseheader.h"

namespace Ui {
class AddVitaminSupplement;
}

class AddVitaminSupplement : public QDialog
{
    Q_OBJECT

public:
    explicit AddVitaminSupplement(QWidget *parent = nullptr);
    ~AddVitaminSupplement();

private slots:
    void on_supplement_save_btn_clicked();

    void on_supplement_reset_btn_clicked();

    void on_supplement_update_btn_clicked();

    void on_supplement_delete_btn_clicked();

private:
    Ui::AddVitaminSupplement *ui;
};

#endif // ADDVITAMINSUPPLEMENT_H
```

```
#include "addvitaminsupplement.h"
#include "ui_addvitaminsupplement.h"

AddVitaminSupplement::AddVitaminSupplement(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::AddVitaminSupplement)
{
    ui->setupUi(this);

}

AddVitaminSupplement::~AddVitaminSupplement()
{
    delete ui;
}

void AddVitaminSupplement::on_supplement_save_btn_clicked()
{
    dconnect conn;
    QString supplementName, supplementType, supplementDescription, supplementAmount;
    supplementName = ui -> supplement_name_lineEdit -> text();
    supplementType = ui -> supplement_type_lineEdit -> text();
    supplementDescription = ui -> supplement_description_textEdit -> toPlainText();
    supplementAmount = ui -> Supplement_amount_lineEdit -> text();

    qDebug() << "영양제 이름 : " << supplementName << "영양제 종류 : " << supplementType << "영양제 설명 : " << supplementDescription << "영양제 가격 : " << supplementAmount;

    if(!conn.connOpen())
    {
        qDebug() << "데이터베이스 연결에 실패 하였습니다.";
        return;
    }

    conn.connOpen();
    QSqlQuery qry;
    qry.prepare("INSERT INTO supplement(Name, Type, Description, Amount) VALUES (:Name,:Type,:Description,:Amount)");
    qry.bindValue(":Name",supplementName);
    qry.bindValue(":Type",supplementType);
    qry.bindValue(":Description",supplementDescription);
    qry.bindValue(":Amount",supplementAmount);

    if(qry.exec( ))
    {
        QSqlDatabase::database().commit();
        QMessageBox::information(this, tr("Save"), tr("Saved"));
        conn.connClose();
    }
    else
    {
        QMessageBox::critical(this, tr("error::"), qry.lastError().text());
    }


}

void AddVitaminSupplement::on_supplement_update_btn_clicked()
{
    dconnect conn;
    QString supplementName, supplementType, supplementDescription, supplementAmount;

    supplementName = ui -> supplement_name_lineEdit -> text();
    supplementType = ui -> supplement_type_lineEdit -> text();
    supplementDescription = ui -> supplement_description_textEdit -> toPlainText();
    supplementAmount = ui -> Supplement_amount_lineEdit -> text();

    if(!conn.connOpen())
    {
        qDebug() << "데이터베이스 연결에 실패 하였습니다.";
        return;
    }

    conn.connOpen();
    QSqlQuery qry;
    qry.prepare("update supplement set Name='"+supplementName+"', Type='"+supplementType+"', Description='"+supplementDescription+"', Amount='"+supplementAmount+"' where Name = '"+supplementName+"'");

    if(qry.exec( ))
    {
        QSqlDatabase::database().commit();
        QMessageBox::information(this, tr("Edit"), tr("Update"));
        conn.connClose();
    }
    else
    {
        QMessageBox::critical(this, tr("error::"), qry.lastError().text());
    }
}


void AddVitaminSupplement::on_supplement_delete_btn_clicked()
{
    dconnect conn;
    QString supplementName;

    supplementName = ui -> supplement_name_lineEdit -> text();

    if(!conn.connOpen())
    {
        qDebug() << "데이터베이스 연결에 실패 하였습니다.";
        return;
    }

    conn.connOpen();
    QSqlQuery qry;
    qry.prepare("Delete from supplement where Name='"+supplementName+"'");

    if(qry.exec( ))
    {
        QSqlDatabase::database().commit();
        QMessageBox::information(this, tr("Delete"), tr("Deleted"));
        conn.connClose();
    }
    else
    {
        QMessageBox::critical(this, tr("error::"), qry.lastError().text());
    }
}

```

```
#include "findvitaminsupplement.h"
#include "ui_findvitaminsupplement.h"

FindVitaminSupplement::FindVitaminSupplement(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::FindVitaminSupplement)
{
    ui->setupUi(this);

}

FindVitaminSupplement::~FindVitaminSupplement()
{
    delete ui;
}


void FindVitaminSupplement::on_find_btn_clicked()
{
    dconnect conn;

    QString Findtype;
    Findtype = ui -> find_type_lineEdit -> text();
    QSqlQueryModel * model = new QSqlQueryModel;

    conn.connOpen();

    QSqlQuery* qry = new QSqlQuery(conn.db);

    qry -> prepare("SELECT Name,Type,Description,Amount FROM supplement where Type like '%" +Findtype + "%' ");

    qry -> exec(); // 얻은 데이터를 위에서 포인터로 정의한 모델로 전송한다.

/*    model -> setQuery(std::move(*qry));*/ //  인수로 위에서 두번째로 생성한 쿼리 객체를 전달한다.
    if(qry ->exec( ))
    {
        QMessageBox::information(this, tr("Save"), tr("Saved"));
        model -> setQuery(std::move(*qry));
        ui->type_tableView->setModel(model);
        qDebug() << (model->rowCount()); // 행 수를 계산하기 위함
        conn.connClose(); // 데이터베이스 닫음
    }
    else
    {
        QMessageBox::critical(this, tr("error::"), qry ->lastError().text());
    }
    // 테이블 뷰에 전달하기 위한 작업
//    ui->type_tableView->setModel(model);

//    ui->type_tableView->resizeRowsToContents();
//    qDebug() << (model->rowCount()); // 행 수를 계산하기 위함
//    conn.connClose(); // 데이터베이스 닫음
//    ui->type_tableView->resizeColumnsToContents();

//    ui->type_tableView->setWordWrap(true);
//    ui->type_tableView->setTextElideMode(Qt::ElideLeft);
//    ui->type_tableView->resizeColumnsToContents();
//    ui->type_tableView->resizeRowsToContents();
//    ui -> type_tableView -> setColumnWidth(0, 200);
//    ui -> type_tableView -> setColumnWidth(1, 200);
//    ui -> type_tableView -> setColumnWidth(2, 500);
//    ui -> type_tableView -> setColumnWidth(3, 500);

//    ui->type_tableView->setWordWrap(true);
//    ui->type_tableView->setTextElideMode(Qt::ElideLeft);
//    ui->type_tableView->resizeColumnsToContents();
//    ui->type_tableView->resizeRowsToContents();




//    model -> setQuery(std::move(Query_Find_Data));
//    ui -> type_tableView -> setModel(model);
//    ui->type_tableView->setWordWrap(true);
//    ui->type_tableView->setTextElideMode(Qt::ElideLeft);
//    ui->type_tableView->resizeColumnsToContents();
//    ui->type_tableView->resizeRowsToContents();


//    db.close();
}

```
![image](https://user-images.githubusercontent.com/115389450/235426869-d9617129-c833-4b73-bf84-0de5fa56dd31.png)



