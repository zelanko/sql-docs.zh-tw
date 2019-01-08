---
title: 建立變數值檔案 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Variable Value File Creation
- Variable Value File, Variable Value File Validation
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 067781fd998c9e7763fe3a9f2befacab59687250
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534052"
---
# <a name="creating-variable-value-files-oracletosql"></a>建立變數值檔案 (OracleToSQL)
變數值檔案是 XML 檔案包含一些來源或目的地伺服器名稱經常變更從一部伺服器移轉到另一個的命令的參數值。 大量的資料庫移轉發生時，會建立並使用主要的指令碼檔案中參考多個變數的檔案，以儲存每個來源伺服器的值 **-v**在命令列切換。 這有助於維護幾個指令碼檔案中的靜態值，與多個變數的檔案中的變數值。  
  
> [!NOTE]  
> 1.  變數名稱會做為前置詞和後置字元為 $ （美元） 符號。 如果變數未指派的變數值檔案中的值，您就會導致懸置在主控台執行程序的指令碼檔案剖析期間發生錯誤。  
> 2.  逸出字元**$** 是**$$**。 如果變數或靜態值的參數值包含**$** （貨幣） 符號，然後**$$** 必須指定將它視為一個字元，而不是變數。  
> 3.  基於可維護性，變數可以宣告內`'variable-group'`邏輯區隔使用者的項目定義的變數。  這個元素的使用方式不是必要的。  
  
**範例：**  
  
**範例 1:**  
  
```  
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
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
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
  
## <a name="next-step"></a>下一個步驟  
操作主控台的下一個步驟是[建立伺服器連線檔案&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器檔案 (Oracle)](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  
