---
title: "安裝沒有網際網路存取的 R 元件 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# 安裝沒有網際網路存取的 R 元件
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所用的 R 元件安裝程式需要網際網路連線，存取 Microsoft 下載中心或其他信任的網站所提供的檔案。 不過，您可以建立本主題描述的本機複本，在沒有網際網路存取的伺服器上安裝這些元件。  
  
  > [!TIP]
  > 
  > 如需離線安裝程序的詳細逐步解說，請參閱 [SQL Server 客戶諮詢小組](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)的部落格。
  
## <a name="installation-on-computers-with-no-internet-access"></a>安裝在沒有網際網路存取的電腦上  
 如果您要執行離線安裝，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 無法存取連結安裝必要的 R 元件。 為避免這個問題，您可以在本機下載安裝程式複本，並依此處描述完成安裝。
 
 請注意，R元件安裝程式有兩個︰一個用於 Microsoft R Open，另一個用於 Microsoft R Server。 這兩個都必須下載並安裝，才能使用 SQL Server R Services。 SQL Server 安裝精靈會確定它們已依正確順序安裝。


版本  |下載連結  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab：](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**如何在離線安裝中更新 R 元件**     

1. 使用上述連結下載適當的版本。
2. 將封包檔複製到您要安裝更新的電腦資料夾中。
3. 當您執行 SQL Server 的安裝精靈時，按一下 [Microsoft R 授權] 頁面的 [接受]。  對話方塊隨即出現，列出下載連結。 輸入所下載檔案的位置路徑。 
4. 按一下 [下一步] 指出元件可供使用，並完成 SQL Server 安裝精靈。
5. 或者，您也可以下載開放原始碼元件的已封存原始程式碼。 如需詳細資訊，請參閱[安裝 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。


> [!IMPORTANT] 如果您將 .cab 檔案當成 SQL Server 安裝程式的一部分下載到能存取網際網路的電腦上，安裝精靈會偵測本機語言並自動變更安裝程式的語言。 
> 
> 不過，如果您要將當地語系化版本的 SQL Server 安裝到無法存取網際網路的電腦上，並將 R 安裝程式下載到本機共用時，您必須手動編輯已下載檔案的名稱並插入您要安裝語言的正確語言識別項。 
> 
> 例如，如果您要安裝日文版的 SQL Server，檔案名稱應該要從 SRS_8.0.3.0_1033.cab 變更成 SRS_8.0.3.0_1041.cab。    
 
  
## <a name="see-also"></a>另請參閱  
 [開始使用 SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [R Services 安裝程式疑難排解](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  