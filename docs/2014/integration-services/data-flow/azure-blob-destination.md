---
title: Azure Blob 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdest.f1
- sql11.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb406d38b17748e8284acee4b2849a9fd99e53ac
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432385"
---
# <a name="azure-blob-destination"></a>Azure Blob 目的地
  [Azure Blob 目的地]  元件可讓 SSIS 封裝將資料寫入 Azure Blob。 支援的檔案格式：CSV 與 AVRO。 拖-將**Azure Blob 目的地**放到資料流程設計師，然後按兩下以查看編輯器）。  
  
1.  針對 [Azure 儲存體連線管理員]**** 欄位，請指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員。  
  
2.  針對 [Blob 容器名稱]**** 欄位，請指定包含原始程式檔的 Blob 容器名稱。  
  
3.  針對 [Blob 名稱]**** 欄位，請指定 Blob 的路徑。  
  
4.  針對 [Blob 檔案格式]**** 欄位，請指定要使用的 Blob 格式。  
  
5.  若檔案格式為 CSV，則您必須指定 [資料行分隔符號字元]**** 值。 如果檔案中的第一個資料列包含資料行名稱，也請選取**第一個資料列中的資料行名稱**。  
  
6.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  
  
  
