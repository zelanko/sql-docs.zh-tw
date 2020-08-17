---
description: '建立變數值檔案 (AccessToSQL) '
title: 建立變數值檔案 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8815b6d3f6d4f825082b0c2eac4d8bfa45cb98de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320874"
---
# <a name="creating-variable-value-files-accesstosql"></a>建立變數值檔案 (AccessToSQL) 
變數值檔案是一種 XML 檔案，其中包含命令的參數值 (例如，通常會在伺服器遷移之間變更的來源或目的地伺服器名稱) 。 發生大量的資料庫移轉時，會在主要腳本檔案中建立多個變數檔案來儲存每個來源伺服器的值，並在命令列中使用 **-v** 參數進行參考。 此行為有助於在多個變數檔案中，以變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> -  變數名稱前面會加上 $ (貨幣) 符號。 如果未在變數值檔案中為變數指派值，則會在剖析腳本檔案期間發生錯誤，而導致拖延主控台執行進程。  
> -  的 escape 字元為 **$** **$$** 。 如果參數的變數或靜態值的值包含 **$** (貨幣) 符號，則 **$$** 必須指定此值，才能將它視為字元而不是變數。  
> -  基於可維護性的目的，您可以在專案內宣告變數， `'variable-group'` 以邏輯分隔使用者自訂變數。  此元素的使用方式不是強制的。  
  
**範例：**  
  
**範例 1：**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**範例 2：**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>變數值檔案驗證  
使用者可以針對 [架構] 資料夾中提供的架構定義檔 **ConsoleScriptVariablesSchema** ，輕鬆地驗證其變數值檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是 [建立伺服器連接檔案 &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連接檔案 (存取) ](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
