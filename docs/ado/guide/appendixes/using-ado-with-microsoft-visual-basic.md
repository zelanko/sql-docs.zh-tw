---
title: 使用 ADO 與 Microsoft Visual Basic |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d409f874e9fcec059c01ddef91d83d8a70fdeb47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864514"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>應用程式搭配使用 ADO 與 Microsoft Visual Basic 和 Visual Basic
設定 ADO 專案，並撰寫 ADO 程式碼很類似您是否使用 Visual Basic 或 Visual Basic 應用程式。 本主題說明使用 Visual Basic 和 Visual Basic 中使用 ADO 的應用程式，並資訊的任何差異。

## <a name="referencing-the-ado-library"></a>參考 ADO 程式庫
 您的專案必須參考 ADO 程式庫。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>若要從 Microsoft Visual Basic 參考 ADO

1.  在 Visual Basic 中從**專案**功能表上，選取**參考...**.

2.  選取 **程式庫的 Microsoft ActiveX Data Objects x.x**從清單中。 確認至少下列的程式庫也會一併選取：

    -   Visual Basic for Applications

    -   Visual Basic 執行階段物件和程序

    -   Visual Basic 物件和程序

    -   OLE Automation

3.  按一下 [確定] 。

 您可以使用 ADO 輕鬆地使用 Visual Basic 應用程式，例如使用 Microsoft Access。

#### <a name="to-reference-ado-from-microsoft-access"></a>若要從 Microsoft Access 中參考 ADO

1.  在 Microsoft Access 中，選取或建立的模組**模組**索引標籤中**資料庫**視窗。

2.  在 **工具**功能表上，選取**參考...**.

3.  選取 **程式庫的 Microsoft ActiveX Data Objects x.x**從清單中。 確認至少下列的程式庫也會一併選取：

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 物件程式庫 （或更新版本）

    -   Microsoft DAO 3.5 物件程式庫 （或更新版本）

4.  按一下 [確定] 。

## <a name="creating-ado-objects-in-visual-basic"></a>在 Visual Basic 中建立 ADO 物件
 若要建立自動化變數和物件，該變數的執行個體，您可以使用兩種方法：**Dim**或是**CreateObject**。

### <a name="dim"></a>維度
 您可以使用**的新**關鍵字搭配**Dim**宣告，並在一個步驟中建立 ADO 物件的執行個體：

```
Dim conn As New ADODB.Connection
```

 或者， **Dim**陳述式宣告和物件具現化也可以是兩個步驟：

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  它不需要明確地使用`ADODB`使用 progid **Dim**陳述式中，假設您已正確參考 ADO 程式庫專案中。 不過，使用它可確保，您不需要命名衝突與其他程式庫。

> [!NOTE]
>  比方說，如果您將 ADO 和 DAO 的參考納入相同的專案時，您應該包含辨識符號，指定要具現化時使用的物件模型**資料錄集**物件，如下列程式碼所示：

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 具有**CreateObject**方法、 宣告和物件具現化必須是兩個獨立的步驟：

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 使用物件具現化**CreateObject**是晚期繫結，這表示它們不強型別且已停用命令列完成。 不過，它確實可讓您略過從您的專案中參考 ADO 程式庫，並可讓您具現化物件的特定版本。 例如：

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 您也可以完成這特別建立的 ADO 版本 2.0 類型程式庫的參考，並建立物件。

 使用具現化物件**CreateObject**方法會比使用通常慢**Dim**陳述式。

## <a name="handling-events"></a>處理事件
 若要處理 ADO 事件 Microsoft Visual Basic 中，您必須宣告模組層級變數 using **WithEvents**關鍵字。 變數可以宣告只為一部分的類別模組，而且必須在模組層級宣告。 處理 ADO 事件的更完整討論，請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。

## <a name="visual-basic-examples"></a>Visual Basic 範例
 許多 Visual Basic 範例隨附的 ADO 文件。 如需詳細資訊，請參閱 < [Microsoft Visual Basic 中的 ADO 程式碼範例](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md)。

## <a name="see-also"></a>另請參閱
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [搭配使用 ADO 與 Microsoft Visual C++ ](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [搭配使用 ADO 與指令碼語言](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
