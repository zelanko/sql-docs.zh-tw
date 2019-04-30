---
title: 建立變數值檔案 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 00144c51e60b72fe043443d2a9c8d1d51a6cb8da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138830"
---
# <a name="creating-variable-value-files-accesstosql"></a>建立變數值檔案 (AccessToSQL)
變數的值，檔案是 XML 檔案包含經常變更整個伺服器的移轉命令 （例如來源或目的地伺服器名稱） 的參數值。 大量的資料庫移轉發生時，建立和主要的指令碼檔案中參考多個變數的檔案，以儲存每個來源伺服器的價值 **-v**在命令列切換。 此行為有助於維護幾個指令碼檔案中的靜態值，與多個變數的檔案中的變數值。  
  
> [!NOTE]  
> -  變數名稱會做為前置詞和後置字元為 $ （美元） 符號。 如果變數未指派的變數值檔案中的值，在指令碼檔案的剖析期間會發生錯誤，導致懸置在主控台執行程序。  
> -  逸出字元**$** 是**$$**。 如果變數或靜態值的參數值包含**$** （貨幣） 符號，然後**$$** 必須指定將它視為一個字元，而不是變數。  
> -  基於可維護性，變數可以宣告內`'variable-group'`使用者定義變數的邏輯分隔的項目。  這個元素的使用方式不是必要的。  
  
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
  
## <a name="variable-value-file-validation"></a>變數值檔案驗證  
使用者可以輕鬆地驗證他/她變數值檔案對結構描述定義檔**ConsoleScriptVariablesSchema.xsd**可用 [結構描述] 資料夾中。  
  
## <a name="next-step"></a>下一步  
操作主控台的下一個步驟是[建立伺服器連線檔案&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連線檔案 （存取）](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
