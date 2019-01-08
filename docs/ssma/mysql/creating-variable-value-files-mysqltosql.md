---
title: 建立變數值檔案 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 73919295dbd53cbaaca3847d5be119e5fe2d0bb7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530146"
---
# <a name="creating-variable-value-files-mysqltosql"></a>建立變數值檔案 (MySQLToSQL)
變數值檔案是 XML 檔案包含一些來源或目的地伺服器名稱經常變更從一部伺服器移轉到另一個的命令的參數值。 大量的資料庫移轉發生時，會建立並使用主要的指令碼檔案中參考多個變數的檔案，以儲存每個來源伺服器的值 **-v**在命令列切換。 這有助於維護幾個指令碼檔案中的靜態值，與多個變數的檔案中的變數值。  
  
> [!NOTE]  
> 1.  變數名稱會做為前置詞和後置字元為 $ （美元） 符號。 如果變數未指派的變數值檔案中的值，您就會導致懸置在主控台執行程序的指令碼檔案剖析期間發生錯誤。  
> 2.  逸出字元**$** 是**$$**。 如果變數或靜態值的參數值包含**$** （貨幣） 符號，然後**$$** 必須指定將它視為一個字元，而不是變數。  
> 3.  基於可維護性，變數可以宣告內`'variable-group'`邏輯區隔使用者的項目定義的變數。  這個元素的使用方式不是必要的。  
  
**範例：**  
  
**範例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
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
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
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
使用者可以輕鬆地驗證他/她變數值檔案對結構描述定義檔 **'ConsoleScriptVariablesSchema.xsd'** 可用 [結構描述] 資料夾中。  
  
## <a name="next-step"></a>下一個步驟  
操作主控台的下一個步驟是[建立伺服器連線檔案&#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連線檔案 (MySQL)](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
