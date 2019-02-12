---
title: DQS 定義域支援的 SQL Server 和 SSIS 資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 566215be603b52e50999bb737451278881274402
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024700"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>DQS 定義域支援的 SQL Server 和 SSIS 資料類型
  有許多資料型別，在 SQL Server 和 SQL Server Integration Services (SSIS)，但只有四個 DQS 定義域資料類型：日期、 Decimal、 Integer 和字串。 DQS 並不支援所有 SQL Server 和 SSIS 資料類型。 只有當 DQS 支援來源資料類型，而且該類型符合 DQS 定義域資料類型時，您才能將來源資料對應至 DQS 定義域，以便執行資料品質活動。 本主題將提供受支援而且可分別對應至 DQS 中四種定義域資料類型之 SQL Server 和 SSIS 資料類型的相關資訊。  
  
> [!NOTE]  
>  在 .xlsx 和 .xls 檔案中，來源資料行的資料類型是由前八個資料列中最普遍的資料類型所決定。 如果資料格不符合該資料類型，將會為它提供 null 值。 同樣地，在 .csv 檔案中，來源資料行的資料類型是由前八個資料列中最普遍的資料類型所決定。  
  
##  <a name="SQLServer"></a> 支援的 SQL Server 資料類型  
 下表將提供每種 DQS 定義域資料類型所支援之 SQL Server 資料類型的相關資訊：  
  
|DQS 定義域資料類型|支援的 SQL Server 資料類型|  
|--------------------------|------------------------------------|  
|date|日期|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> REAL<br /><br /> SMALLMONEY|  
|Integer|BIGINT<br /><br /> ssNoversion<br /><br /> smallint<br /><br /> TINYINT|  
|String|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 DQS 不支援其餘 SQL Server 資料類型。 如需所有 SQL Server 資料類型的資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)。  
  
##  <a name="SSIS"></a> 支援的 SSIS 資料類型  
 下表將提供每種 DQS 定義域資料類型所支援之 SSIS 資料類型的相關資訊：  
  
|DQS 定義域資料類型|支援的 SSIS 資料類型|  
|--------------------------|------------------------------|  
|date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 DQS 不支援其餘 SSIS 資料類型。 如需有關所有 SSIS 資料類型的資訊，請參閱＜ [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [管理網域](../../2014/data-quality-services/managing-a-domain.md)  
  
  
