---
description: 建立變數值檔案 (MySQLToSQL)
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
ms.openlocfilehash: b612ec00ecebf5dd9e4cd2cf803567f1d7dfc149
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988441"
---
# <a name="creating-variable-value-files-mysqltosql"></a>建立變數值檔案 (MySQLToSQL)
變數值檔案是一個 XML 檔案，其中包含命令的參數值，例如，通常會從一部伺服器遷移到另一個伺服器的來源或目的地伺服器名稱。 發生大量的資料庫移轉時，系統會在命令列中使用 **-v** 參數，在主腳本檔案中建立並參考用來儲存每個來源伺服器值的多個變數檔案。 這有助於在多個變數檔案中，以變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> 1.  變數名稱前面會加上 $ (貨幣) 符號。 如果變數未在變數值檔案中指派值，則在剖析腳本檔案期間，將會發生錯誤，導致拖延主控台執行進程。  
> 2.  的 escape 字元為 **$** **$$** 。 如果參數的變數或靜態值的值包含 **$** (貨幣) 符號，則 **$$** 必須指定此值，才能將它視為字元而不是變數。  
> 3.  基於可維護性的目的，您可以在專案內宣告變數， `'variable-group'` 以邏輯分隔使用者定義的變數。  此元素的使用方式不是強制的。  
  
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
使用者可以根據 [架構] 資料夾中提供的架構定義檔 **' ConsoleScriptVariablesSchema .xsd '** ，輕鬆地驗證其變數值檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是 [建立伺服器連接檔案 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[ (MySQL) 建立伺服器連接檔案 ](./creating-the-server-connection-files-mysqltosql.md)  
