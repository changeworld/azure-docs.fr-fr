---
title: Comment configurer OpenVPN sur une passerelle VPN Azure
description: Découvrez comment utiliser PowerShell pour activer le protocole OpenVPN sur la passerelle VPN Azure pour un environnement de point à site.
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: how-to
ms.date: 02/05/2021
ms.author: cherylmc
ms.openlocfilehash: 4b48e98ab35b620030b15165d4c9341c0f11b440
ms.sourcegitcommit: d4734bc680ea221ea80fdea67859d6d32241aefc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100393273"
---
# <a name="configure-openvpn-for-azure-point-to-site-vpn-gateway"></a>Configurer OpenVPN pour la passerelle VPN Azure de point à site

Cet article vous aide à configurer le **protocole OpenVPN®** sur la passerelle VPN Azure. Vous pouvez utiliser le portail ou les instructions PowerShell.

## <a name="prerequisites"></a>Prérequis

* Nous partons du principe que vous disposez déjà d’un environnement de point à site fonctionnel. Autrement, créez-en un à l’aide de l’une des méthodes suivantes.

  * [Portail – Créer une connexion point à site](vpn-gateway-howto-point-to-site-resource-manager-portal.md)

  * [PowerShell – Créer une connexion point à site](vpn-gateway-howto-point-to-site-rm-ps.md)

* Vérifiez que votre passerelle VPN n’utilise pas la référence (SKU) de base. La référence De base n’est pas prise en charge pour OpenVPN.

## <a name="portal"></a>Portail

1. Dans le portail, accédez à votre **Passerelle de réseau virtuel -> Configuration point à site**.
1. Sous **Type de tunnel**, sélectionnez **OpenVPN (SSL)** dans la liste déroulante.

   :::image type="content" source="./media/vpn-gateway-howto-openvpn/portal.png" alt-text="Sélectionnez OpenVPN SSL dans la liste déroulante.":::
1. Enregistrez vos modifications et passez aux **Étapes suivantes**.

## <a name="enable-openvpn-on-your-gateway-using-powershell"></a>Activez OpenVPN sur votre passerelle à l'aide de PowerShell.

1. Activez OpenVPN sur votre passerelle en suivant l’exemple suivant :

   ```azurepowershell-interactive
   $gw = Get-AzVirtualNetworkGateway -ResourceGroupName $rgname -name $name
   Set-AzVirtualNetworkGateway -VirtualNetworkGateway $gw -VpnClientProtocol OpenVPN
   ```
1. Passez aux **Étapes suivantes**.

## <a name="next-steps"></a>Étapes suivantes

Pour configurer les clients pour OpenVPN, consultez [Configurer les clients OpenVPN](vpn-gateway-howto-openvpn-clients.md).

**« OpenVPN » est une marque d’OpenVPN Inc.**
