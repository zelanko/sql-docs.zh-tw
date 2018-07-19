---
title: 建立變數值檔案 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3865c268ef4da360b5e21cba96e88ddf6028ae6a
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773804"
---
# <a name="creating-variable-value-files-accesstosql"></a>建立變數值檔案 (AccessToSQL)
變數的值，檔案是 XML 檔案中所包含的參數值經常變更整個伺服器移轉的命令 （例如來源或目的地伺服器名稱）。 大量的資料庫移轉發生時，建立並與主要指令碼檔案中參考多個變數的檔案，以儲存每個來源伺服器的值 **– v**在命令列參數。 這個行為有助於維護幾個指令碼檔案中的多個變數的檔案中的變數值的靜態值。  
  
> [!NOTE]  
> -  變數名稱會做為前置詞和後置字元為 $ （美元） 符號。 如果變數未指派的變數值檔案中的值，在指令碼檔剖析期間會發生錯誤，導致一主控台執行程序。  
> -  The escape character for **$** is **$$**. 如果變數或靜態值的參數值包含**$** （美元） 符號，然後**$$** 必須指定以將其視為一個字元，而不是變數。  
> -  為了可維護性，變數可以宣告內`‘variable-group’`邏輯隔離的使用者定義變數的項目。  使用這個項目不是強制性。  
  
**範例：**  
  
**範例 1:**  
  
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
**範例 2:**  
  
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
  
## <a name="variable-value-file-validation"></a>變數值的檔案驗證  
使用者可以輕鬆地驗證其變數值檔案對結構描述定義檔**ConsoleScriptVariablesSchema.xsd**可用 '結構描述' 資料夾中。  
  
## <a name="next-step"></a>下一步  
在操作主控台的下一個步驟是[伺服器連線檔案建立&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連接檔案 (Access)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
