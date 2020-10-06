---
description: 在 IIS 上設定虛擬伺服器
title: 在 IIS 上設定虛擬伺服器 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: b8e1899e6393f1dc7ae4d9b2080d349bbedf1d41
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724789"
---
# <a name="configuring-virtual-servers-on-iis"></a>在 IIS 上設定虛擬伺服器
在 Internet Information Services 4.0 中建立虛擬伺服器時，需要下列兩個額外的步驟，才能將虛擬伺服器設定為使用 RDS：  
  
1.  設定伺服器時，請核取 [允許執行存取]。  
  
2.  將 msadcs.dll 移至 *vroot*\msadc，其中 *vroot* 是您虛擬伺服器的主目錄。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)