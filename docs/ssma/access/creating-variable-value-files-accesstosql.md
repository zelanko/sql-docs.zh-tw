---
title: 建立變數值檔案（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 051ded7d675f81998718b858c71488ba968ec680
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006600"
---
# <a name="creating-variable-value-files-accesstosql"></a>建立變數值檔案（AccessToSQL）
變數值檔案是一個 XML 檔案，其中包含經常跨伺服器遷移而變更的命令參數值（例如來源或目的地伺服器名稱）。 當發生大量的資料庫移轉時，會在命令列上使用 **-v**參數來建立及參考用於儲存每個來源伺服器值的多個變數檔案。 這個行為有助於以多個變數檔案中的變數值來維護一些腳本檔案中的靜態值。  
  
> [!NOTE]  
> -  變數名稱前面會加上 $ （美元）符號的前置詞和尾碼。 如果變數未獲指派變數值檔案中的值，則會在剖析腳本檔案期間發生錯誤，而導致主控台執行程式停止。  
> -  的逸出字元**$** 為**$$**。 如果參數的變數或靜態值值包含**$** （美元）符號，則**$$** 必須將它指定為將它視為字元，而不是變數。  
> -  基於可維護性的考慮，變數可以`'variable-group'`在專案內宣告，以進行使用者定義變數的邏輯分隔。  此元素的使用不是強制的。  
  
**範例：**  
  
**範例 1：**  
  
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
**範例2：**  
  
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
使用者可以針對 [架構] 資料夾中提供的架構定義檔**ConsoleScriptVariablesSchema** ，輕鬆地驗證其變數值檔案。  
  
## <a name="next-step"></a>後續步驟  
操作主控台的下一個步驟是[&#40;AccessToSQL 建立伺服器連接檔案&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[建立伺服器連接檔案（存取）](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
