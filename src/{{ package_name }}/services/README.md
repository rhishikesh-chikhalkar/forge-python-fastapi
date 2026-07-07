# Services Layer

This package contains **use-case orchestration** — the application-level
logic that coordinates domain objects, repositories, and external services
to fulfill a user request.

## Rules

1. **One service per use-case** — keep services focused.  A `CreateOrderService`
   should not also handle order cancellation.

2. **Depend on abstractions** — inject repository interfaces (from
   `repositories/base.py`), not concrete implementations.

3. **Transaction boundaries** — services own the transaction scope.  Start a
   DB session, call repositories, commit or rollback.

4. **No HTTP concepts** — services must not import `Request`, `Response`, or
   HTTP status codes.  Those belong in `views/`.

## Example

```python
class CreateOrderService:
    def __init__(self, order_repo: OrderRepository, payment_gateway: PaymentGateway):
        self.order_repo = order_repo
        self.payment_gateway = payment_gateway

    async def execute(self, user_id: UUID, items: list[OrderItem]) -> Order:
        order = Order.create(user_id=user_id, items=items)
        await self.payment_gateway.charge(order.total)
        await self.order_repo.save(order)
        return order
```
