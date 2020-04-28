---
title: 建立變數值檔案（OracleToSQL） |Microsoft Docs
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
manager: shamikg
ms.openlocfilehash: 87db0ebd006e2ca87ddc4744a4bbcd396a827712
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266116"
---
# <a name="creating-variable-value-files-oracletosql"></a>建立變數值檔案 (OracleToSQL)
變數值檔案是一種 XML 檔案，其中包含命令的參數值，例如來源或目的地伺服器名稱，通常會從一部伺服器遷移到另一個伺服器。 當發生大量的資料庫移轉時，將會在命令列上使用 **-v**參數來建立及參考用於儲存每個來源伺服器值的多個變數檔案。 這有助於使用多個變數檔案中的變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> 1.  變數名稱前面會加上 $ （美元）符號的前置詞和尾碼。 如果變數不是指派給變數值檔案中的值，您在剖析腳本檔案期間會發生錯誤，而導致停止主控台執行程式。  
> 2.  的逸出字元**$** 為**$$**。 如果參數的變數或靜態值值包含**$** （美元）符號，則**$$** 必須指定，以將它視為字元，而不是變數。  
> 3.  基於可維護性的考慮，變數可以`'variable-group'`在專案內宣告，以進行使用者定義變數的邏輯分隔。  此元素的使用不是強制的。  
  
**範例：**  
  
**範例 1：**  
  
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
**範例2：**  
  
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
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[&#40;OracleToSQL 建立伺服器連接檔案&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器檔案（Oracle）](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  
