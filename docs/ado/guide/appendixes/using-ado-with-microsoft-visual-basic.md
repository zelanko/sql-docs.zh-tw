---
title: "使用 ADO 搭配 Microsoft Visual Basic |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c88dbb57318fe960eab28c463b8c46a5546ffd5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Microsoft Visual Basic 和 Visual Basic 中使用 ADO 的應用程式
設定 ADO 專案，並撰寫 ADO 程式碼相似的。 您是否使用 Visual Basic 或 Visual Basic 應用程式 本主題說明使用 Visual Basic 和 Visual Basic 使用 ADO 的應用程式，並且資訊的任何差異。

## <a name="referencing-the-ado-library"></a>ADO 程式庫的參考
 ADO 程式庫必須由您的專案參考。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>若要從 Microsoft Visual Basic 參考 ADO

1.  在 Visual Basic 中，從**專案**功能表上，選取**參考...**.

2.  選取**Microsoft ActiveX Data Objects x.x 文件庫**從清單中。 確認至少也會選取下列的程式庫：

    -   Visual Basic for Applications

    -   Visual Basic 執行階段物件和程序

    -   Visual Basic 物件和程序

    -   OLE Automation

3.  按一下 **[確定]**。

 您可以使用 ADO 很容易與 Visual Basic 應用程式，例如使用 Microsoft Access。

#### <a name="to-reference-ado-from-microsoft-access"></a>若要從 Microsoft Access 參考 ADO

1.  在 Microsoft Access 中，選取或建立的模組**模組**索引標籤中**資料庫**視窗。

2.  在**工具**功能表上，選取**參考...**.

3.  選取**Microsoft ActiveX Data Objects x.x 文件庫**從清單中。 確認至少也會選取下列的程式庫：

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 物件程式庫 （或更新版本）

    -   Microsoft DAO 3.5 物件程式庫 （或更新版本）

4.  按一下 **[確定]**。

## <a name="creating-ado-objects-in-visual-basic"></a>在 Visual Basic 中建立 ADO 物件
 若要建立的自動化變數和物件，該變數的執行個體，您可以使用兩種方法： **Dim**或**CreateObject**。

### <a name="dim"></a>維度
 您可以使用**新增**關鍵字搭配**Dim**宣告，並以一個步驟建立 ADO 物件的執行個體：

```
Dim conn As New ADODB.Connection
```

 或者， **Dim**陳述式宣告和物件具現化也可以是兩個步驟：

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  不需要明確使用`ADODB`progid 與**Dim**陳述式中，假設您已正確地在專案中參考 ADO 程式庫。 不過，使用它可確保，您不需要其他程式庫與命名衝突。

> [!NOTE]
>  例如，如果您在相同的專案包含 ADO 和 DAO 的參考，您應該包含辨識符號指定具現化時所要使用哪一個物件模型**資料錄集**物件，如下列程式碼所示：

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 與**CreateObject**方法、 宣告和物件具現化必須是離散的兩個步驟：

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 使用物件具現化**CreateObject**是晚期繫結，也就是說，它們不強型別，並已停用命令列完成。 不過，它確實可讓您略過您的專案，從參考 ADO 程式庫，並可讓您具現化物件的特定版本。 例如：

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 您也無法完成此作業藉由明確建立 ADO 版本 2.0 類型程式庫的參考，並建立物件。

 使用具現化物件**CreateObject**方法低於通常使用**Dim**陳述式。

## <a name="handling-events"></a>處理事件
 若要處理 ADO 事件在 Microsoft Visual Basic，您必須宣告模組層級變數使用**WithEvents**關鍵字。 變數可以宣告只能為類別模組的一部分，但必須在模組層級中宣告。 處理 ADO 事件的更完整討論，請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。

## <a name="visual-basic-examples"></a>Visual Basic 範例
 許多 Visual Basic 範例隨附的 ADO 文件。 如需詳細資訊，請參閱[ADO 程式碼範例在 Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)。

## <a name="see-also"></a>另請參閱
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [使用 ADO 搭配 Microsoft Visual c + +](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [使用 ADO 搭配指令碼語言](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

