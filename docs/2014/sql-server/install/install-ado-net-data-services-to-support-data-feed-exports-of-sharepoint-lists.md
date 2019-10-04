---
title: 安裝 ADO.NET 資料服務以支援 SharePoint 清單的資料摘要匯出 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9b3ec2d8b7459f9d66313c6a40b1cbc26450e0d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952159"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>如何：安裝 ADO.NET Data Services 以支援 SharePoint 清單的資料摘要匯出
  從 SharePoint 清單匯出資料摘要需要 ADO.NET Data Services。 SharePoint 2010 不會在 SharePoint 必要安裝程式中包含這個元件，所以您必須手動安裝它。  
  
 若沒有此必要條件，當您嘗試使用匯出為數據摘要的 SharePoint 清單時，將會收到下列錯誤：「基於安全性理由，在此 XML 檔中禁止 DTD。 若要啟用 DTD 處理，請將 XmlReaderSettings 上的 ProhibitDtd 屬性設定為 false，並且將這項設定傳入 XmlReader.Create 方法。」  
  
 使用下列程序，在您想要讓清單當做資料摘要匯出的每一部 SharePoint 伺服器上安裝 ADO.NET Data Services。  
  
### <a name="download-and-install-adonet-data-services"></a>下載及安裝 ADO.NET Data Services  
  
1.  前往 SharePoint 2010 的硬體和軟體需求檔、[硬體和軟體需求（sharepoint 2010）](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  在 [**存取適用的軟體**] 中，尋找對應到您所使用之作業系統（Windows SERVER 2008 SP2 或 windows Server 2008 R2）之 ADO.NET 資料服務3.5 的連結。  
  
3.  按一下該連結，並執行安裝程式來安裝服務。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
