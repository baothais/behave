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
          
 _Feature:_
  - Feature là từ khóa dùng để mô tả về chức năng/User store được định nghĩa các trường hợp kiểm thử trong file *.feature. Tất cả các file "*.feature" được quy ước chỉ bao gồm một feature
 
 _Scenario:_
  - Scenario là nòng cốt trong cấu trúc Gherkin, nó là các kịch bản phản ánh các hoạt động test trong một TestCase

  - Mọi Scenario đều bắt đầu với từ khóa "Scenario:" theo sau bởi một nội dung tùy ý - thường sẽ là tên của testcase hay nội dung muốn test

  - Mỗi Feature có thể có một hoặc nhiều Scenario, và mỗi Scenario bao gồm một hay nhiều Step.

  - Ví dụ:

        Scenario: The User subscribe with Email was used to subscription system
            Given I am staying Testmaster homepage
             When I try to subscribe with "khanh.tx@live.com" email
             Then I should see "E-mail khanh.tx@live.com đã được sử dụng, bạn hãy chọn một E-mail khác"

        Scenario: The User subscribe with Email is not in used on subscription system
            Given I am staying Testmaster homepage
             When I try to subscribe with "khanh.tx@testmaster.vn" email
             Then I should see "Bạn đã đăng ký nhận tin thành công, vui lòng check mail để kích hoạt."
             
_Background:_
 - Background là keyword cho phép them một vài context vào tất cả các scenario trong một file feature.

 - Một background được viết giống như Scenario không có tiêu đề và bao gồm một số Step.

 - Sự khác nhau giữa background và Scenario là background chạy trước mỗi Scenario, nhưng sau các Hook (@Before) cách thức hoạt động giống với @BeforeMethod trong TestNG

 - Ví dụ:

       Feature: Send News to Subscribers

        Background:
             Given I open the request to admin page
               And I provide my email "khanh.tx@live.com" and my password "abc123" to login

        Scenario: Administator create News in the past
            Given I am staying subscription manager
             When I try to create News with time to send in the past
             Then I should see "Bạn không thể chọn thời điểm gửi trong quá khứ."

        Scenario: Administrator create News in the future
            Given I am staying subscription manager
             When I try to create News with time to send in the future
             Then I should see the News display on News list
_Step:_
 - Feature bao gồm các Step như: Givens, Whens, Thens...
  
_Given:_
 - Được sử dụng để mô tả ngữ cảnh ban đầu của hệ thống/chức năng. Mục đích của Given là đưa hệ thống/chức năng vào mọt trạng thái đã biết trước khi sử dụng (giả thiết), trước khi bắt đầu tương tác với hệ thống.

_When:_
 - Là từ khóa (keyword) sử dụng để mô tả các sự kiện, hành động chính mà người dùng sử dụng.

_Then:_
 - Sử dụng Then để mô tả các kết quả mong muốn tương ứng với ngữ cảnh/testcase.

_And, But:_
 - Khi có nhiều Given, When, Then thì có thể dùng các từ khóa And hoặc But để kết hợp các điều kiện.

_Chú ý:_ Trong mỗi một Scenario 3 từ khóa chính Given, When, Then chỉ nên xuất hiện một lần duy nhất

_Comment:_
 - Trong feature file ta có thể đánh dấu một nội dung bất kỳ là một comment (dòng nội dung không được thực thi) bằng cách đặt dấu "#" ở đầu dòng.

_Step Definition:_
 - Cucumber không thể biết làm thế nào để thực thi được một Scenario đã được định nghĩa trong file Feature. Nó cần Step Definition để biên dịch nguyên văn các bước Gherkin thành các hành động tương tác với hệ thống qua WebDriver

 - Khi Cucumber thực thi các Step trong Scenario, nó sẽ tìm kiếm các Step Definition phù hợp đề thực thi thông qua các Annotation tương ứng

 - Để hiểu Step Definition làm việc, hãy xem ví dụ sau:

_Feature File:_

    Feature: As a user I want to subscribe with my Email sothat I can get the news which provided by system

      Scenario: Subscribe with existed Email then see the popup message
         Given I open the page with subscription function
          When I provide the email already subscribed before such as "khanh.tx@live.com"
           And I submit my information
          Then The user should see the notification "E-mail khanh.tx@live.com đã được sử dụng, bạn hãy chọn một E-mail khác"

_Step Definition:_

    @RunWith(Cucumber.class)
    public class MyStepDefinitions {

       @Given("^I open the page with subscription function$")
       public void iOpenThePageWithSubscriptionFunction() throws Throwable {
            throw new PendingException();
       }

       @When("^I provide the email already subscribed before such as \"([^\"]*)\"$")
       public void iProvideTheEmailAlreadySubscribedBeforeSuchAsSomething(String strArg1) throws Throwable {
            throw new PendingException();
       }
       @Then("^The user should see the notification \"([^\"]*)\"$")
       public void theUserShouldSeeTheNotificationSomething(List list1) throws Throwable {
            throw new PendingException();
       }

       @And("^I submit my information$")
       public void iSubmitMyInformation() throws Throwable {
            throw new PendingException();
       }
    }
  
  
  
  
  
  
  
  
  
  
  
  
  

