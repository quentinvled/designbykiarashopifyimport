<div class="quantity-discount-selector">
  <!-- Affichage des paliers de remise -->
  <div class="discount-tiers">
    <h3>Économisez plus en achetant plusieurs !</h3>
    <div class="tier-badges">
      <span class="tier-badge" data-qty="2">
        <strong>2 articles</strong>
        <span class="discount">-10%</span>
      </span>
      <span class="tier-badge" data-qty="3">
        <strong>3 articles</strong>
        <span class="discount">-15%</span>
      </span>
      <span class="tier-badge" data-qty="4">
        <strong>4+ articles</strong>
        <span class="discount">-20%</span>
      </span>
    </div>
    <p class="discount-notice" style="display: none;">
      <small>✓ Promotion appliquée automatiquement dans le panier</small>
    </p>
  </div>

  <!-- Affichage dynamique du prix -->
  <div class="price-display">
    <div class="price-row">
      <span class="price-label">Prix unitaire :</span>
      <span class="price-value">{{ product.price | money }}</span>
    </div>

    <div class="price-row total-row">
      <span class="price-label">
        Total pour <span class="qty-display">1</span> article<span class="qty-plural"></span> :
      </span>
      <span class="price-value">
        <span class="original-total" style="display: none;"></span>
        <span class="final-total">{{ product.price | money }}</span>
      </span>
    </div>

    <div class="savings-row" style="display: none;">
      <span class="savings-label">Économie réalisée :</span>
      <span class="savings-value"></span>
    </div>
  </div>
</div>

<style>
.quantity-discount-selector {
  margin: 20px 0;
  font-family: inherit;
}

.discount-tiers {
  background: 
#FFFFFF;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  border: 1px solid 
#e5e5e5;
}

.discount-tiers h3 {
  margin: 0 0 15px 0;
  font-size: 16px;
  color: #000;
  font-weight: 600;
}

.tier-badges {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  margin-bottom: 12px;
}

.tier-badge {
  background: 
#FAFAFA;
  border: 2px solid 
#e5e5e5;
  padding: 10px 16px;
  border-radius: 6px;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
}

.tier-badge.active {
  border-color: #000;
  background: #000;
  color: white;
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  animation: badgeActivate 0.4s ease-out;
}

@keyframes badgeActivate {
  0% {
    transform: translateY(0) scale(1);
    box-shadow: 0 0 0 rgba(0,0,0,0);
  }
  50% {
    transform: translateY(-4px) scale(1.08);
    box-shadow: 0 6px 20px rgba(0,0,0,0.25);
  }
  100% {
    transform: translateY(-2px) scale(1.05);
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  }
}

.tier-badge.active strong,
.tier-badge.active .discount {
  color: white;
}

.tier-badge strong {
  font-size: 14px;
  color: #333;
  font-weight: 500;
}

.tier-badge .discount {
  color: #000;
  font-weight: bold;
  font-size: 18px;
  margin-top: 4px;
}

.discount-notice {
  margin: 0;
  color: #666;
  font-size: 13px;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-5px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes pulse {
  0% {
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  }
  50% {
    box-shadow: 0 4px 12px rgba(0,0,0,0.2), 0 0 0 8px rgba(0,0,0,0.1);
  }
  100% {
    box-shadow: 0 4px 12px rgba(0,0,0,0.2), 0 0 0 12px rgba(0,0,0,0);
  }
}

.price-display {
  margin-top: 20px;
  padding: 20px;
  background: 
#FFFFFF;
  border-radius: 8px;
  border: 1px solid 
#e5e5e5;
}

.price-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
  font-size: 14px;
}

.price-row.total-row {
  font-size: 16px;
  font-weight: 600;
  padding-top: 12px;
  border-top: 1px solid 
#e5e5e5;
  margin-top: 12px;
  margin-bottom: 0;
}

.price-label {
  color: #666;
}

.total-row .price-label {
  color: #000;
}

.price-value {
  color: #000;
  font-weight: 500;
}

.original-total {
  text-decoration: line-through;
  color: #999;
  margin-right: 8px;
  font-weight: normal;
}

.final-total {
  color: #000;
  font-weight: 600;
}

.savings-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 12px;
  padding-top: 12px;
  border-top: 1px dashed 
#e5e5e5;
  animation: fadeIn 0.3s ease;
}

.savings-label {
  color: #666;
  font-size: 14px;
}

.savings-value {
  color: #000;
  font-weight: 600;
  font-size: 14px;
}

/* Animation pour le changement de prix */
.price-value, .savings-value {
  transition: all 0.3s ease;
}

/* Responsive */
@media (max-width: 480px) {
  .tier-badges {
    gap: 8px;
  }

  .tier-badge {
    padding: 8px 12px;
  }

  .tier-badge strong {
    font-size: 12px;
  }

  .tier-badge .discount {
    font-size: 16px;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Sélecteurs pour le composant quantity-input de Shopify
  const quantityInput = document.querySelector('quantity-input .quantityinput');
  const minusBtn = document.querySelector('.quantitybutton[name="minus"]');
  const plusBtn = document.querySelector('.quantity__button[name="plus"]');

  // Éléments d'affichage
  const tierBadges = document.querySelectorAll('.tier-badge');
  const qtyDisplay = document.querySelector('.qty-display');
  const qtyPlural = document.querySelector('.qty-plural');
  const originalTotal = document.querySelector('.original-total');
  const finalTotal = document.querySelector('.final-total');
  const savingsRow = document.querySelector('.savings-row');
  const savingsValue = document.querySelector('.savings-value');
  const discountNotice = document.querySelector('.discount-notice');

  // Prix unitaire en centimes (pour éviter les problèmes de float)
  const unitPrice = {{ product.price }};

  // Fonction pour obtenir le pourcentage de remise
  function getDiscountPercent(qty) {
    if (qty >= 4) return 20;
    if (qty === 3) return 15;
    if (qty === 2) return 10;
    return 0;
  }

  // Fonction pour mettre à jour l'affichage
  function updateDisplay() {
    const qty = parseInt(quantityInput.value) || 1;
    const discountPercent = getDiscountPercent(qty);

    // Mettre à jour les badges actifs avec animation
    tierBadges.forEach(badge => {
      const badgeQty = parseInt(badge.dataset.qty);
      if ((badgeQty === 4 && qty >= 4) || (badgeQty === qty)) {
        // Ajouter la classe avec un petit délai pour déclencher l'animation
        if (!badge.classList.contains('active')) {
          badge.classList.add('active');
          // Effet de pulsation supplémentaire
          badge.style.animation = 'none';
          setTimeout(() => {
            badge.style.animation = 'badgeActivate 0.4s ease-out, pulse 0.6s ease-out';
          }, 10);
        }
      } else {
        badge.classList.remove('active');
      }
    });

    // Afficher/masquer la notice de promotion avec animation
    if (discountPercent > 0) {
      if (discountNotice.style.display === 'none') {
        discountNotice.style.display = 'block';
        discountNotice.style.animation = 'fadeIn 0.4s ease-out';
      }
    } else {
      discountNotice.style.display = 'none';
    }

    // Calculer les prix
    const subtotal = unitPrice * qty;
    const discountAmount = Math.round(subtotal * discountPercent / 100);
    const total = subtotal - discountAmount;

    // Mettre à jour l'affichage des quantités
    qtyDisplay.textContent = qty;
    qtyPlural.textContent = qty > 1 ? 's' : '';

    // Mettre à jour les prix avec animation
    if (discountPercent > 0) {
      originalTotal.style.display = 'inline';
      originalTotal.textContent = Shopify.formatMoney(subtotal);
      savingsRow.style.display = 'flex';
      savingsValue.textContent = Shopify.formatMoney(discountAmount) + ' (-' + discountPercent + '%)';
    } else {
      originalTotal.style.display = 'none';
      savingsRow.style.display = 'none';
    }

    // Animation du prix final
    finalTotal.style.opacity = '0.5';
    setTimeout(() => {
      finalTotal.textContent = Shopify.formatMoney(total);
      finalTotal.style.opacity = '1';
    }, 150);
  }

  // Gestionnaires d'événements pour le champ input
  if (quantityInput) {
    quantityInput.addEventListener('input', updateDisplay);
    quantityInput.addEventListener('change', updateDisplay);

    // Gestionnaires pour les boutons + et -
    if (minusBtn) {
      minusBtn.addEventListener('click', function() {
        setTimeout(updateDisplay, 10);
      });
    }

    if (plusBtn) {
      plusBtn.addEventListener('click', function() {
        setTimeout(updateDisplay, 10);
      });
    }

    // Clic sur les badges pour sélectionner directement une quantité
    tierBadges.forEach(badge => {
      badge.addEventListener('click', function() {
        const qty = parseInt(this.dataset.qty);
        quantityInput.value = qty;

        // Déclencher l'événement input pour que Shopify mette à jour ses composants
        const event = new Event('input', { bubbles: true });
        quantityInput.dispatchEvent(event);

        updateDisplay();

        // Petit effet visuel sur le sélecteur de quantité
        quantityInput.style.transform = 'scale(1.1)';
        setTimeout(() => {
          quantityInput.style.transform = 'scale(1)';
        }, 200);
      });
    });

    // Initialisation
    updateDisplay();
  }
});
</script>