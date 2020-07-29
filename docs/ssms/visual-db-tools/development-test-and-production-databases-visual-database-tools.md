---
title: 開發、測試和生產資料庫
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e0f50cc149c592633969c84a8f541239d55f1240
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85986878"
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>開發、測試和生產資料庫 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
如果您有兩個結構完全相同的資料庫，您可以變更其中一個資料庫，然後再將這些變更傳播到另一個資料庫。 例如，如果您具備個人開發資料庫和群組測試資料庫，您可以修改開發資料庫，然後將這些變更傳播到測試資料庫。  
  
若要完成此工作，請在單一工作階段中對開發資料庫執行所有的修改，建立工作階段的變更指令碼 (Change Script)，然後在測試資料庫中執行此指令碼。  
  
## <a name="see-also"></a>另請參閱  
[多使用者環境 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
