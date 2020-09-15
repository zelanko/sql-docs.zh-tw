---
description: 使用加密
title: 使用加密
ms.custom: Learn how to establish secure communication channels using TLS encryption with your SQL database connections.
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86a36cec5930630c00501796e9c2340106cfa6c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414574"
---
# <a name="using-encryption"></a>使用加密

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

傳輸層安全性 (TLS) 可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體與用戶端應用程式之間傳輸加密的資料。  
  
傳輸層安全性 (TLS) 是一種通訊協定，可建立安全地通訊通道來防止重要或機密的資訊透過網路和其他網際網路通訊遭到攔截。 TLS 可讓用戶端與伺服器驗證彼此的身分。 參與者經過驗證後，TLS 會在用戶端和伺服器之間提供加密的連線以便進行安全的訊息傳輸。  
  
[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會提供一個基礎結構，根據使用者指定的連線屬性和伺服器與用戶端的設定，啟用和停用特定連線的加密。 使用者可以指定憑證存放區位置和密碼、用於驗證憑證的主機名稱，以及加密通訊通道的時機。  
  
對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體與應用程式之間網路上傳輸的資料，啟用 TLS 加密可提高其安全性。 不過，啟用加密確實會減緩效能。  
  
本節中的主題將描述 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 版本如何支援 TLS 加密 (包括新的連線屬性)，以及如何在用戶端設定信任的存放區。  
  
> [!NOTE]  
> 建議使用 **hostNameInCertificate** 連接屬性來驗證 TLS 憑證。  

## <a name="in-this-section"></a>本節內容  

| 主題                                                                                                        | 描述                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [了解加密支援](../../connect/jdbc/understanding-ssl-support.md)                                 | 描述 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 如何支援 TLS 加密。                                              |
| [使用加密連線](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | 描述如何使用新的 TLS 特定連線屬性連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 |
| [為用戶端設定加密](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | 描述如何在用戶端設定預設的信任存放區，以及如何將私用憑證匯入到用戶端電腦的信任存放區中。   |
  
## <a name="see-also"></a>另請參閱

[保護 JDBC 驅動程式應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
