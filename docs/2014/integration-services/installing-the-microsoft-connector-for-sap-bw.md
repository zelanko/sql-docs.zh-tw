---
title: 安裝 Microsoft Connector for 1.1 SAP BW |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: dc6bbbf5972615880d3852d5f56a955862c9f22b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145664"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>安裝 Microsoft Connector for 1.1 SAP BW
  若要安裝[!INCLUDE[msCoName](../includes/msconame-md.md)]Connector 1.1 for SAP BW 及其文件，下載及執行 SQL Server 功能套件網頁上的 Windows installer 套件。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
## <a name="required-sap-files"></a>必要的 SAP 檔案  
 若要使用[!INCLUDE[msCoName](../includes/msconame-md.md)]Connector 1.1 for SAP BW，您不需要在本機電腦上安裝 SAP 前端軟體 (SAP GUI)。  
  
 不過，您必須將 SAP .NET Connector 檔案 librfc32.dll 複製到 Windows 資料夾的系統子資料夾中 (通常此資料夾的位置是 **C:\Windows\system32**)。  
  
## <a name="considerations-for-64-bit-computers"></a>64 位元電腦的考量  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 完全支援 64 位元版本的[!INCLUDE[msCoName](../includes/msconame-md.md)]Windows。 64 位元電腦上， [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 具有下列額外需求：  
  
-   若要在 64 位元 Windows 作業系統上以 64 位元模式執行封裝，請將 64 位元版本的 SAP GUI 檔案 librfc32.dll 複製到 Windows 資料夾的 **system32** 資料夾中 (通常此檔案的位置是 **C:\Windows\system32**)。  
  
-   若要在 64 位元 Windows 作業系統上以 32 位元模式執行封裝，請將 SAP GUI 檔案 librfc32.dll 複製到 Windows 資料夾的 **SysWow64** 資料夾中 (通常此資料夾的位置是 **C:\Windows\SysWow64**)。  
  
  