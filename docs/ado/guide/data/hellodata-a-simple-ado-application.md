---
title: HelloData：簡單的 ADO 應用程式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f9f0cd227a258b1d2d9cd2d201527f614bcc49
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758824"
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData：簡易 ADO 應用程式
這個簡單的應用程式會逐步解說四個主要 ADO 作業：取得、檢查、編輯和更新資料。 這些作業會針對 Microsoft® SQL Server 隨附的 Northwind 範例資料庫執行。 為了專注于 ADO 的基本概念，並防止程式碼雜亂，範例中的錯誤處理是最小的。  
  
### <a name="to-run-hellodata"></a>若要執行 HelloData  
  
1.  建立參考 ADO 程式庫的新標準 EXE Visual Basic 專案。 如需詳細資訊，請參閱[參考 ADO 程式庫](../../../ado/guide/referencing-the-ado-libraries.md)。  
  
2.  在表單頂端建立四個命令按鈕，將 [**名稱**] 和 [**標題**] 屬性設定為本主題結尾表中顯示的值。  
  
3.  在按鈕下方新增**Microsoft DataGrid 控制項**（Msdatgrd）。 Msdatgrd 隨附于 Visual Basic，並位於您的 \windows\system32 或 \winnt\system32 目錄中。 若要將 DataGrid 控制項加入至 Visual Basic 的 [工具箱] 窗格，請從 [**專案**] 功能表選取 [**元件**]。 然後核取 [Microsoft DataGrid Control 6.0 （SP3）（OLEDB）] 旁的方塊，然後按一下 **[確定]**。 若要將控制項加入至專案，請將 DataGrid 控制項從 [工具箱] 拖曳至 [Visual Basic] 表單。  
  
4.  在方格下方的表單上建立**TextBox** ，並設定其屬性，如下表所示。 當您完成時，表單應如下圖所示。  
  
5.  最後，複製[HelloData 程式碼](../../../ado/guide/data/hellodata-code.md)中所列的程式碼，並將它貼入表單的 [程式碼編輯器] 視窗中。 按**F5**執行程式碼。  
  
> [!NOTE]
>  在下列範例中，和整個指南中，會使用密碼為 "123aBc" 的使用者識別碼 "MyId" 來對伺服器進行驗證。 您應該以伺服器的有效登入認證來取代這些值。 此外，請將 "MySQLServer" 值替換為您的伺服器名稱。  
  
 如需程式碼的詳細描述，請參閱[HelloData 上的批註](../../../ado/guide/data/comments-on-hellodata.md)。  
  
 ![顯示 HelloData VB 應用程式的 Form1](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|控制項類型|屬性|值|  
|------------------|--------------|-----------|  
|表單|Name|Form1|  
||高度|6500|  
||寬度|6500|  
|MS DataGrid|Name|grdDisplay1|  
|TextBox|Name|txtDisplay1|  
||多行|true|  
|命令按鈕|Name|cmdGetData|  
||Caption|取得資料|  
|命令按鈕|Name|cmdExamineData|  
||Caption|檢查資料|  
|命令按鈕|Name|cmdEditData|  
||Caption| 編輯資料|  
|命令按鈕|Name|cmdUpdateData|  
||Caption|更新資料|
