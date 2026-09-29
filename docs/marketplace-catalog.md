# 🛒 Marketplace, Catalog & Search

## Product Lifecycle

```mermaid
flowchart LR
    A[Draft] --> B[Pending Review] --> C[Published]
    C --> D[Paused]
    C --> E[Out of Stock]
    D --> C
    E --> C
    C --> F[Archived]
```

## Product Data

| Area | Details |
|---|---|
| Variants | Size, color, material, customization, quantity |
| Media | Multiple photos, optional video, cover selection |
| Details | Title, description, category, tags, price, stock, dimensions, weight, shipping info |

## Search & Discovery

- **Search fields:** title, description, category, tags, artisan name, material
- **Filters:** category, price, availability, rating, craft type, customization, delivery region
- **Natural-language search:** describe what you want in plain words
- **Visual search:** upload an image to find related products

## Recommendations

Similar products • From this artisan • Related craft • Recently viewed • Personalized (with privacy controls)

## Trust Information

Seller profile • Verification state • Reviews • Shipping policy • Return policy

## Sharing

Deep links / shareable product URLs for external sharing.

See also: [Features](features.md) · [AI System](ai-system.md)
