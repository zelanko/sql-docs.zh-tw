---
title: 使用資料庫鏡像端點憑證 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 116c5d900cf56d89c01bbf333d2d8bd3905aa371
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754020"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>使用資料庫鏡像端點憑證 (Transact-SQL)
  若要啟用某伺服器執行個體上資料庫鏡像的憑證驗證，系統管理員必須設定每一個伺服器執行個體，才能同時在傳出和傳入的連接使用憑證。 您必須先設定傳出連接。  
  
> [!NOTE]  
>  伺服器執行個體上的所有鏡像連接都使用單一資料庫鏡像端點，而您必須在建立端點時指定伺服器執行個體的驗證方法。 因此，您可以在每一個伺服器執行個體只使用一個驗證形式進行資料庫鏡像。  
  
## <a name="configuring-outbound-connections"></a>設定傳出連接  
 在每一個您要設定資料庫鏡像的伺服器執行個體上依照下列步驟進行：  
  
1.  在 **master** 資料庫中，建立資料庫主要金鑰。  
  
2.  在 **master** 資料庫中，建立伺服器執行個體的加密憑證。  
  
3.  使用伺服器執行個體的憑證來建立其端點。  
  
4.  將憑證備份至檔案中，並以安全的方式將其複製到其他一或多個系統。  
  
 您必須為每一個夥伴或見證 (如果有的話) 完成上述步驟。  
  
 如需詳細資訊，請參閱 [允許資料庫鏡像端點使用輸出連線的憑證 &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)。  
  
## <a name="configuring-inbound-connections"></a>設定傳入連接  
 接著，在每一個您要設定資料庫鏡像的夥伴上依照下列步驟進行。 在 **master** 資料庫中：  
  
1.  為其他系統建立登入。  
  
2.  為該登入建立使用者。  
  
3.  取得另一個伺服器執行個體的鏡像端點的憑證。  
  
4.  使憑證與步驟 2 所建立的使用者產生關聯。  
  
5.  將 CONNECT 權限授與登入，以連接該鏡像端點。  
  
 如果有見證，您也必須為它設定傳入連接。 這需要在兩個夥伴上設定見證的登入、使用者和憑證，反之亦然。  
  
 如需詳細資訊，請參閱 [允許資料庫鏡像端點使用輸入連線的憑證 &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)。  
  
## <a name="security"></a>安全性  
 除非您可保證網路的安全無虞，否則建議您對資料庫鏡像連接使用加密。 如需詳細資訊，請參閱 [資料庫鏡像端點 &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)。  
  
 將憑證複製到另一個系統時，請使用安全複製方法。 務必將您所有的憑證小心保管。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料庫主要金鑰](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [資料庫鏡像和 AlwaysOn 可用性群組的傳輸安全性 &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [資料庫鏡像端點 &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
  
  
