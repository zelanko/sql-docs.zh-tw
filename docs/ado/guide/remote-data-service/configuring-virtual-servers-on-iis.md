---
title: "在 IIS 上設定虛擬伺服器 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10edd98f77c0aaeae05d25e76ad76a15b99bc1ed
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-virtual-servers-on-iis"></a>在 IIS 上設定虛擬伺服器
在建立虛擬伺服器在網際網路資訊服務 4.0 中，設定才能使用 RDS 虛擬伺服器所需下列兩個額外的步驟：  
  
1.  設定伺服器，請檢查 「 允許執行存取 」。  
  
2.  移至 msadcs.dll *vroot*\msadc，其中*vroot*是您的虛擬伺服器的主目錄。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)



