---
title: 多語言及全域部署 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 12e796619f7ab5674f5f94b34ea15d4e2aefe595
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>多語言及全域部署 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 可部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援之所有語言的元件和工具。 如需相關資訊，請參閱 [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
## <a name="how-languages-are-used"></a>如何使用語言  
 下表描述 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 元件和工具的語言支援。  
  
|元件或工具|描述|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安裝程式|當您希望 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式所提供及支援的語言與安裝程式語言不同時，請選取英文安裝程式。 如需詳細資訊，請參閱底下的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 描述。|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|安裝程式語言會決定 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 語言。 例如，如果您選擇德文當做安裝程式語言，該電腦上就會提供德文的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|當您執行英文版的安裝程式時，將會提供及支援所有應用程式語言版本的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 應用程式。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 可以在任何一種應用程式語言中顯示，並根據用戶端網頁瀏覽器的語言喜好設定來接受地區設定特有的輸入。 如果針對不支援的應用程式語言來設定語言喜好設定， [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 會預設為英文。<br /><br /> 當您執行英文版以外的安裝程式時，其他所有應用程式語言都會包含資源，但是用戶端如果使用選定安裝程式語言以外之語言版本的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ，就不會受到支援。 如果您嘗試存取安裝程式語言以外之語言版本的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ，您可能會遇到應用程式內資料顯示和輸入的問題。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 資料庫內的資訊並不是任何地區設定所特有。 如此可讓 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 決定如何使用用戶端 Web 瀏覽器語言喜好設定所決定的格式來顯示資訊，例如日期和數字。|  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
