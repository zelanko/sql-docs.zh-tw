---
title: 建立變數值檔案（SybaseToSQL） |Microsoft Docs
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
ms.openlocfilehash: 2c0c76a36502d9d590b6db478efcab6feb50ba01
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029396"
---
# <a name="creating-variable-value-files-sybasetosql"></a>建立變數值檔案 (SybaseToSQL)
變數值檔案是一種 XML 檔案，其中包含命令的參數值，例如來源或目的地伺服器名稱，通常會從一部伺服器遷移到另一個伺服器。 當發生大量的資料庫移轉時，將會在命令列上使用 **-v**參數來建立及參考用於儲存每個來源伺服器值的多個變數檔案。 這有助於使用多個變數檔案中的變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> 1.  變數名稱前面會加上 $ （美元）符號的前置詞和尾碼。 如果變數不是指派給變數值檔案中的值，您在剖析腳本檔案期間會發生錯誤，而導致停止主控台執行程式。  
> 2.  的逸出字元**$** 為**$$**。 如果參數的變數或靜態值值包含**$** （美元）符號，則**$$** 必須指定，以將它視為字元，而不是變數。  
> 3.  基於可維護性的考慮，變數可以`'variable-group'`在專案內宣告，以進行使用者定義變數的邏輯分隔。  此元素的使用不是強制的。  
  
**範例：**  
  
**範例 1：**  
  
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
**範例2：**  
  
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
使用者可以針對 [架構] 資料夾中提供的架構定義檔**ConsoleScriptVariablesSchema** ，輕鬆地驗證其變數值檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[&#40;SybaseToSQL 建立伺服器連接檔案&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器檔案（Sybase）](https://msdn.microsoft.com/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  
