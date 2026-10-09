1. **SRP (Single Responsibility):** Clases enfocadas en un único objetivo (`OrderService`, `PaymentService`, `NotificationService`).
2. **OCP (Open/Closed):** Extensión de pasarelas de pago mediante interfaces.
3. **LSP (Liskov Substitution):** Reemplazo transparente entre contratos de pago (`YapePayment`, `PlinPayment`, `CardPayment`).
4. **ISP (Interface Segregation):** Interfaces pequeñas y específicas (`Payment`, `IInvoice`, `IRefund`).
5. **DIP (Dependency Inversion):** Dependencia de abstracciones mediante inyección de dependencias.
