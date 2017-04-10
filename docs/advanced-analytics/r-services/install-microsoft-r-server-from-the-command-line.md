---
title: "從命令列安裝 Microsoft R Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# 從命令列安裝 Microsoft R Server
    
您可以使用 SQL Server 安裝程式所提供的指令碼功能，從命令列安裝 Microsoft R Server。 

- **自動**安裝需要您指定安裝程式公用程式的位置，並使用引數表示要安裝的功能。 
- 針對**無訊息**安裝，提供相同引數，並新增 **/q** 參數。 將不會提供任何提示，也不需要任何互動。 不過，如果省略任何必要引數，則安裝程式會失敗。

如需詳細資訊，請參閱 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

## <a name="perform-a-command-line-install-of-microsoft-r-server-standalone"></a>執行 Microsoft R Server 的命令列安裝 (獨立)

 下列範例顯示在使用 SQL Server 安裝程式執行 Microsoft R Server 命令列安裝時所使用的引數。


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>R Server 獨立自動安裝的範例

從提升權限的命令提示字元執行下列命令，僅安裝 Microsoft R Server (獨立) 和其必要條件。 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

若要檢視進度和提示，請移除 /q 引數。

請注意，需要下列所有引數：
  - **FEATURES = SQL_SHARED_MR** 只會取得 Microsoft R Server 元件 (包括 Microsoft R Open 和任何必要條件)。
  - **IACCEPTROPENLICENSETERMS** 表示您已接受授權合約以使用開放原始碼 R 元件。
  - 需要有 **IACCEPTSQLSERVERLICENSETERMS**，才能執行安裝精靈。


### <a name="offline-installation"></a>離線安裝

如果您在沒有網際網路存取的電腦上安裝 Microsoft R Server (獨立)，則必須事先下載必要的 R 元件，並將它們複製到本機資料夾。 如需下載位置，請參閱[安裝沒有網際網路存取的 R 元件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。   


## <a name="advanced-installation-tips"></a>進階安裝提示

安裝程式完成之後，您可以檢閱 SQL Server 安裝程式所建立的組態檔，以及安裝程式動作的摘要。

預設會在 `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log` 中建立 SQL Server 的所有安裝程式記錄檔和摘要以及相關功能。

會為安裝的每個功能建立個別的子資料夾。 針對 Microsoft R Server，尋找： 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

若要使用相同的參數來設定另一個 Microsoft R Server 執行個體，您也可以重複使用在安裝期間建立的組態檔。 如需詳細資訊，請參閱[使用組態檔安裝 SQL Server](https://msdn.microsoft.com/library/dd239405.aspx)



### <a name="customizing-your-r-environment"></a>自訂 R 環境

安裝之後，您可以安裝其他 R 套件。 如需詳細資訊，請參閱[安裝和管理 R 套件](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。

> [!IMPORTANT]
> 如果您想要在 SQL Server 上執行 R 程式碼，請確定在執行 Microsoft R Server 的用戶端電腦以及執行 R 服務的 SQL Server 執行個體上安裝相同的套件。 



## <a name="see-also"></a>另請參閱  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  