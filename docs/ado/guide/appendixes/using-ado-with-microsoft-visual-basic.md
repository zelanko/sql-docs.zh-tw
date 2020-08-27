---
description: 搭配使用 ADO 與 Microsoft Visual Basic 和 Visual Basic for Applications
title: 搭配使用 ADO 與 Microsoft Visual Basic |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e2076732536c8d9862ebc022f7a78b197ff428c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990969"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>搭配使用 ADO 與 Microsoft Visual Basic 和 Visual Basic for Applications
無論您使用 Visual Basic 或 Visual Basic for Applications，設定 ADO 專案和撰寫 ADO 程式碼都很類似。 本主題討論如何搭配使用 ADO 與 Visual Basic 和 Visual Basic for Applications，並注意任何差異。

## <a name="referencing-the-ado-library"></a>參考 ADO 程式庫
 您的專案必須參考 ADO 程式庫。

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>參考 Microsoft Visual Basic 的 ADO

1.  在 Visual Basic 中，從 [ **專案** ] 功能表選取 [ **參考 ...**]。

2.  從清單中選取 [ **Microsoft ActiveX Data Objects x.x 程式庫** ]。 確認至少也選取了下列程式庫：

    -   Visual Basic for Applications

    -   Visual Basic 執行時間物件和程式

    -   Visual Basic 物件和程式

    -   OLE Automation

3.  按一下 [確定]。

 例如，您可以使用 Microsoft Access，輕鬆地搭配 Visual Basic for Applications 使用 ADO。

#### <a name="to-reference-ado-from-microsoft-access"></a>從 Microsoft Access 參考 ADO

1.  在 Microsoft Access 中，從 [**資料庫**] 視窗的 [**模組**] 索引標籤中選取或建立模組。

2.  在 [ **工具** ] 功能表上選取 [ **參考 ...**]。

3.  從清單中選取 [ **Microsoft ActiveX Data Objects x.x 程式庫** ]。 確認至少也選取了下列程式庫：

    -   Visual Basic for Applications

    -   Microsoft Access 8.0 物件程式庫 (或更新版本) 

    -   Microsoft DAO 3.5 物件程式庫 (或更新版本) 

4.  按一下 [確定]。

## <a name="creating-ado-objects-in-visual-basic"></a>在 Visual Basic 中建立 ADO 物件
 若要建立自動化變數和該變數之物件的實例，您可以使用下列兩種方法： **Dim** 或 **CreateObject**。

### <a name="dim"></a>變暗
 您可以使用 **New** 關鍵字搭配 **Dim** ，在一個步驟中宣告和建立 ADO 物件的實例：

```
Dim conn As New ADODB.Connection
```

 或者， **維度** 語句宣告和物件具現化也可以是兩個步驟：

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  `ADODB`假設您已在專案中正確參考 ADO 程式庫，則不需要明確地搭配**Dim**語句使用 progid。 不過，使用它可確保您不會與其他程式庫發生名稱衝突。

> [!NOTE]
>  例如，如果您在相同專案中包含 ADO 和 DAO 的參考，則應該包含辨識符號來指定具現化 **記錄集** 物件時所要使用的物件模型，如下列程式碼所示：

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 使用 **CreateObject** 方法時，宣告和物件具現化必須是兩個離散的步驟：

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 使用 **CreateObject** 具現化的物件是晚期繫結的，這表示它們不是強型別，且已停用命令列完成。 不過，它可以讓您略過從專案參考 ADO 程式庫，並讓您具現化特定版本的物件。 例如：

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 您也可以藉由特別建立 ADO 2.0 版類型程式庫的參考，並建立物件來完成這項工作。

 使用 **CreateObject** 方法來具現化物件的速度通常會比使用 **Dim** 語句慢。

## <a name="handling-events"></a>處理事件
 為了處理 Microsoft Visual Basic 中的 ADO 事件，您必須使用 **WithEvents** 關鍵字宣告模組層級變數。 變數只能宣告為類別模組的一部分，而且必須在模組層級宣告。 如需處理 ADO 事件的更完整討論，請參閱 [處理 Ado 事件](../data/handling-ado-events.md)。

## <a name="visual-basic-examples"></a>Visual Basic 範例
 ADO 檔中包含許多 Visual Basic 範例。 如需詳細資訊，請參閱 [Microsoft Visual Basic 中的 ADO 程式碼範例](../../reference/ado-api/ado-code-examples-in-visual-basic.md)。

## <a name="see-also"></a>另請參閱
 [Microsoft ActiveX Data Objects (ado) ](../../microsoft-activex-data-objects-ado.md)搭配使用 ado [與 MICROSOFT VISUAL C++](./using-ado-with-microsoft-visual-c.md)搭配 [使用 ado 與指令碼語言](./using-ado-with-scripting-languages.md)