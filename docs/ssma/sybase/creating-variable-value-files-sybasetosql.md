---
title: 建立變數值檔案 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a172018d136df39c0eb27d8f19b17c783524fe0c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664197"
---
# <a name="creating-variable-value-files-sybasetosql"></a>建立變數值檔案 (SybaseToSQL)
變數值檔案是 XML 檔案包含一些來源或目的地伺服器名稱經常變更從一部伺服器移轉到另一個的命令的參數值。 大量的資料庫移轉發生時，會建立並使用主要的指令碼檔案中參考多個變數的檔案，以儲存每個來源伺服器的值 **– v**在命令列切換。 這有助於維護幾個指令碼檔案中的靜態值，與多個變數的檔案中的變數值。  
  
> [!NOTE]  
> 1.  變數名稱會做為前置詞和後置字元為 $ （美元） 符號。 如果變數未指派的變數值檔案中的值，您就會導致懸置在主控台執行程序的指令碼檔案剖析期間發生錯誤。  
> 2.  逸出字元**$** 是**$$**。 如果變數或靜態值的參數值包含**$** （貨幣） 符號，然後**$$** 必須指定將它視為一個字元，而不是變數。  
> 3.  基於可維護性，變數可以宣告內`‘variable-group’`邏輯區隔使用者的項目定義的變數。  這個元素的使用方式不是必要的。  
  
**範例：**  
  
**範例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**範例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>變數值檔案驗證  
使用者可以輕鬆地驗證他/她變數值檔案對結構描述定義檔**ConsoleScriptVariablesSchema.xsd**可用 [結構描述] 資料夾中。  
  
## <a name="next-step"></a>下一個步驟  
操作主控台的下一個步驟是[建立伺服器連線檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器檔案 (Sybase)](https://msdn.microsoft.com/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  
