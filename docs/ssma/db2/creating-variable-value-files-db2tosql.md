---
description: '建立變數值檔案 (DB2ToSQL) '
title: 建立變數值檔案 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 69753bb7f8b873ebdd74a8c18262034557844c55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463488"
---
# <a name="creating-variable-value-files-db2tosql"></a>建立變數值檔案 (DB2ToSQL) 
變數值檔案是一個 XML 檔案，其中包含命令的參數值，例如，通常會從一部伺服器遷移到另一個伺服器的來源或目的地伺服器名稱。 發生大量的資料庫移轉時，系統會在命令列中使用 **-v** 參數，在主腳本檔案中建立並參考用來儲存每個來源伺服器值的多個變數檔案。 這有助於在多個變數檔案中，以變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> 1.  變數名稱前面會加上 $ (貨幣) 符號。 如果變數未在變數值檔案中指派值，則在剖析腳本檔案期間，將會發生錯誤，導致拖延主控台執行進程。  
> 2.  的 escape 字元為 **$** **$$** 。 如果參數的變數或靜態值的值包含 **$** (貨幣) 符號，則 **$$** 必須指定此值，才能將它視為字元而不是變數。  
> 3.  基於可維護性的目的，您可以在專案內宣告變數， `'variable-group'` 以邏輯分隔使用者定義的變數。  此元素的使用方式不是強制的。  
  
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
**範例 2：**  
  
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
操作主控台的下一個步驟是 [建立伺服器連接檔案 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連線檔案](../oracle/creating-the-server-connection-files-oracletosql.md)  
  
