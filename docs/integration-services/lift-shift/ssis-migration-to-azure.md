---
title: SQL Server Integration Services 移轉至 Azure 概觀 | Microsoft Docs
description: 本文著重於將 SQL Server Integration Services 移轉至 Azure 的程序與工具。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81fb9b9cb792cf350137a375e7a2e25643656b6e
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002849"
---
# <a name="migrate-on-premises-ssis-workloads-to-ssis-in-adf"></a>將內部部署 SSIS 工作負載移轉至 ADF 中的 SSIS

本文列出可協助將 SQL Server Integration Services (SSIS) 工作負載移轉至 ADF 中 SSIS 的程序與工具。

[移轉概觀](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview) (機器翻譯) 著重於將 ETL 工作負載從內部部署 SSIS 移轉至 ADF 中 SSIS 的程序與工具。

移轉程序由兩個階段組成：[評定](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#assessment)及[移轉](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration)。

## <a name="assessment"></a>評量

Data Migration Assistant (DMA) 是可免費下載的工具，適用於此用途，並可在本機安裝及執行。 您可建立 Integration Services 類型的 DMA 評量專案，以批次評定 SSIS 套件並識別出相容性問題。

取得[資料庫移轉小幫手](https://docs.microsoft.com/sql/dma/dma-overview)並[執行套件評定](https://docs.microsoft.com/sql/dma/dma-assess-ssis)。

## <a name="migration"></a>遷移

根據來源 SSIS 套件的儲存體類型，以及資料庫工作負載的移轉目的地，移轉 SSIS 套件與排程 SSIS 套件執行的 SQL Server Agent 作業可能會有不同步驟。 如需詳細資訊，請參閱 [此頁面](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration)。

## <a name="next-steps"></a>後續步驟

- [將 SSIS 套件移轉至 Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance) (機器翻譯)。
- [使用 SQL Server Management Studio (SSMS) 將 SSIS 作業移轉至 Azure Data Factory (ADF)](https://docs.microsoft.com/azure/data-factory/how-to-migrate-ssis-job-ssms) (機器翻譯)。
