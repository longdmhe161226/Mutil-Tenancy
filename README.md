# Hiểu về multi-tenancy

- **Multi-Tenancy** là một mẫu kiến trúc trong [SaaS](https://github.com/longdmhe161226/SaaS/blob/main/README.md) - phần mềm hướng dịch vụ.
- Nó xác định và kiểm soát khách hàng truy cập vào tài nguyên một cách an toàn và hiệu quả.
- Ứng dụng sẽ được tùy chỉnh cho từng khách hàng theo nhu cầu của họ.

## 2-side của hệ thống multi-tenancy
   + **Tenant**: được gọi là Khách hàng sử dụng hệ thống và trả tiền cho nó, Mỗi tenant có user và data riêng được cô lập khỏi các Tenant khác.
   + **Host**: Doanh nghiệp quản lý hệ thống và các Tenant.

## Database
Có 2 cách thiết kế cơ bản nhất là chia sẻ từ một database duy nhất hoặc phân tách database cho mỗi Tenant.
- Sử dụng một database duy nhất: Tất cả data của khách hàng được lưu trữ trong một database được chia sẻ nhưng phải chú ý khi cô lập dữ liệu của các Tenant.
- Database (hoặc schema) cho mỗi khách hàng: Mỗi tenant có một database riêng. Ở cách này cần phải tạo một Connection String riêng cho mỗi Tenant.
- Phương pháp kết hợp: Trong phương pháp này, một số Tenant có database riêng trong khi các Tenant khác được nhóm lại trong một hoặc nhiều database.

- Các thành phần chính của hạ tầng multi-tenancy của ABP:
  
![ABP Multi-Tenancy Infrastructure](https://github.com/longdmhe161226/Mutil-Tenancy/assets/100985816/31639c84-343f-4d83-a1eb-f1df72d49e90)

- Mục tiêu của ABP
Mục tiêu của ABP là tự động hóa logic liên quan đến multi-tenancy càng nhiều càng tốt, làm cho ứng dụng không phụ thuộc vào multi-tenancy. ABP xác định Tenant từ domain/subdomain, cookie, HTTP header,... Sau đó tự động chọn connection nếu Tenant đấy có connection riêng. Nếu Tenant sử dụng database chia sẻ, nó sẽ tự động lọc dữ liệu để khách hàng không vô tình truy cập vào dữ liệu của Tenant khác.

**Tóm lại**: Hiểu đơn giản như có một có nhiều Khách hàng (tenant) họ sử dụng chung một app nhưng data lại độc lập và tách biệt nhau.
