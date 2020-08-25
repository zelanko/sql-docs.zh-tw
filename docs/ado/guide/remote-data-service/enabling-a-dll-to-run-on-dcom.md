---
description: 啟用 DLL 以在 DCOM 上執行
title: 啟用 DLL 以在 DCOM 上執行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: rothja
ms.author: jroth
ms.openlocfilehash: e0c68a6e438f44bedae3134253c72fe49521b44e
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759781"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>啟用 DLL 以在 DCOM 上執行
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列步驟概述如何啟用商務物件 .dll，以透過元件服務使用 DCOM 和 Microsoft Internet Information Services (HTTP) 。  
  
1.  在 [元件服務] MMC 嵌入式管理單元中建立新的空白套件。  
  
     您將使用 [元件服務] MMC 嵌入式管理單元來建立封裝，並將 DLL 加入此封裝中。 這會使 .dll 可透過 DCOM 來存取，但它會移除透過 IIS 的協助工具。  (如果您簽入 .dll 的登錄， **Inproc** 索引鍵現在是空的;設定啟用屬性（本主題稍後將會說明），會在 **Inproc** 索引鍵中新增值。 )   
  
2.  將商務物件安裝到套件中。  
  
     -或-  
  
     將 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件匯入封裝中。  
  
3.  **在建立者的進程** (程式庫應用程式) 中，將封裝的啟用屬性設定為。  
  
     若要使 .dll 可透過相同電腦上的 DCOM 和 IIS 來存取，您必須在 [元件服務] MMC 嵌入式管理單元中設定元件的啟用屬性。 當您 **在建立者的進程中**將屬性設為之後，您會發現登錄中的 **Inproc** 伺服器機碼已加入至元件服務的代理 .dll。  
  
 如需有關元件服務 (或 Microsoft 交易服務的詳細資訊，如果您使用 Windows NT) 以及如何執行這些步驟，請造訪 Microsoft Transaction Server 網站。