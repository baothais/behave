# Gherkin

_Khi sử dụng Gherkin chúng ta chú ý 02 quy tắc sau:_
- Một file Gherkin chỉ mô tả cho một feature/chức năng của chương trình.
- File chứa các Scenario luôn có phần mở rộng là .feature

_Định nghĩa:_ 
 - Gherkin là một ngôn ngữ kịch bản được sử dụng để định nghĩa logic theo cấu trúc với số lượng giới hạn các từ khóa (keyword) được xây dựng sẵn. Bắt đầu một file sẽ là Feature - Mô tả về chức năng mà ta muốn xây dựng các Scenario, sau đó đến Scenario - Các kịch bản kiểm thử, và Steps - Các bước thực hiện theo kịch bản (scenario)
 - Một file feature hợp lệ (không sai về cú pháp), khi chạy mỗi step sẽ match với một code block được định nghĩa trong file mã nguồn sử dụng các ngôn ngữ lập trình như Java/Ruby/Python gọi là "Step Definitions"

_Cú pháp:_

    Feature: As a user I want to subscribe with my Email sothat I can get the news which provided by system
   
      Scenario: Subscribe with existed Email then see the popup message
         Given I open the page with subscription function
          When I provide the email already subscribed before such as "khanh.tx@live.com"
           And I submit my information
          Then The user should see the notification "E-mail khanh.tx@live.com đã được sử dụng, bạn hãy chọn một E-mail khác"
  

