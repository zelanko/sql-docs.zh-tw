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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b3b44a99893c2dbc3dbd3a0597e6600020211702
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935707"
---
# <a name="creating-variable-value-files-mysqltosql"></a>建立變數值檔案 (MySQLToSQL)
變數值檔案是一種 XML 檔案，其中包含命令的參數值，例如來源或目的地伺服器名稱，通常會從一部伺服器遷移到另一個伺服器。 當發生大量的資料庫移轉時，將會在命令列上使用 **-v**參數來建立及參考用於儲存每個來源伺服器值的多個變數檔案。 這有助於使用多個變數檔案中的變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> 1.  變數名稱前面會加上 $ (貨幣) 符號的前置詞和尾碼。 如果變數不是指派給變數值檔案中的值，您在剖析腳本檔案期間會發生錯誤，而導致停止主控台執行程式。  
> 2.  的逸出字元為 **$** **$$** 。 如果參數的變數或靜態值值包含 **$** (貨幣) 符號，則 **$$** 必須指定為將它視為字元，而不是變數。  
> 3.  基於可維護性的考慮，變數可以在專案內宣告， `'variable-group'` 以進行使用者定義變數的邏輯分隔。  此元素的使用不是強制的。  
  
**範例：**  
  
**範例 1：**  
  
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
**範例 2：**  
  
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
使用者可以針對 [架構] 資料夾中提供的架構定義檔 **' ConsoleScriptVariablesSchema** ，輕鬆地驗證其變數值檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[&#40;MySQLToSQL 建立伺服器連接檔案&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[ (MySQL 建立伺服器連接檔案) ](https://msdn.microsoft.com/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
