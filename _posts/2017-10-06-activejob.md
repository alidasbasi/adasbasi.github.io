---
layout: post
title: ActiveJob
tags: [ activejob, rails ]
---

ActiveJob bir Rails kütüphanesidir. ActiveJob ile işleri tanımlarız ve ActiveJob, bizim için işleri arka planda çeşitli sıralama yöntemleri ile sıraya koyup, eş zamanlı olarak çalıştırmaktadır. ActiveJob'un bizim açımızdan en büyük faydalarından biri işlerimizi hızlı bir şekilde gerçekleştirmemizdir. 

ActiveJob ile yapılabilecek işlere örnek verecek olursak; planlı işlerden faturalandırmaya, mail gönderme, kayıt eklemeye kadar bir çok iş yapılabilir.

ActiveJob Rails'in 4.2 sürümünde gelmiş, 5.0 sürümünde çeşitli geliştirmeler yapılarak daha kullanışlı hale gelmiştir. Eğer makinenize Rails yüklü ise ActiveJob'u ayrıca yüklemenize gerek yoktur. Eğer Rails kurulu değilse;

```bash
$ gem install activejob
```

komutu ile kurulumu gerçekleştirebirsiniz. Rails ile yapacağımız projelerde görev oluşturma için aşağıdaki
komutu girmemiz yeterlidir. Rails bu komut ile **app/job** ve **test/job** klasörleri altında birer dosya oluşturacaktır.

```bash
$ rails generate job GenerateRandomUser
invoke  test_unit
create    test/jobs/generate_random_user_job_test.rb
create  app/jobs/generate_random_user_job.rb
```

Bir çalışma üzerinde açıklamak ActiveJob'u anlamak için daha faydalı olacaktır. Çalışmanın kodlarını [adresinden](https://github.com/adasbasi/agenda) ulaşabilirsiniz. Çalışmayı kısaca özetlersek, sistem random olarak ürettiği isim, soyisim ve email her tıkladığınızda iki saniye arayla veritabanına kaydetmesidir.

Çalışmanın **app/controllers/user_controller.rb** dosyası aşağıdaki gibidir.

```ruby
def create
  @user = User.new
  @user.first_name = Faker::Name.first_name
  @user.last_name = Faker::Name.last_name
  @user.email = Faker::Internet.email

  @user.save!
  sleep 2
  redirect_to root_path
end
```

Bu kodlar ile ActiveJob kullanılmadan her kayıt için 2 saniye beklenilmesi gerekecektir. ActiveJob kullanıldıktan sonra ise her tıkladığızda işlemlerin daha hızlı yürüdüğünü göreceksiniz. ActiveJob etkinleştirmek için önce **config/application.rb** üzerinde küçük bir ayar yapmamız lazım, daha sonra **generate_random_user_job.rb** dosyasını düzenleyeceğiz.

```ruby
module Agenda
  class Application < Rails::Application
    config.active_job.queue_adapter = :async # Rails ile ön tanımlı olarak geliyor
    
    config.load_defaults 5.1

  end
end
```

```ruby
class GenerateRandomUserJob < ApplicationJob
  queue_as :default

  def perform(*args)
    # Do something later
    @user = User.new
    @user.first_name = Faker::Name.first_name
    @user.last_name = Faker::Name.last_name
    @user.email = Faker::Internet.email

    @user.save!
    sleep 2
  end
end
```

Ayarımızı yapıp, görevimizi oluşturduktan sonra **user_controller.rb** dosyasını aşağıdaki gibi düzenliyoruz.

```ruby
def create
  GenerateRandomUserJob.perform_later
  redirect_to root_path
end
```

Rails sunucusunu çalıştırdıktan sonra işlerin daha hızlı yürüdğünü göreceksiniz. Aşağıdaki video anlatmak istediğim olayın videosu bulunmaktadır. Bu yazıda kısaca ActiveJob'un ne işe yaradığını anlatmaya çalıştım. ActiveJob haha ayrıntılı bilgiler içeren bir yapıya sahiptir Aşağı vermiş olduğum linklerden daha geniş kapsamlı bilgilere ulaşabilirsiniz.

[![Video](https://www.youtube.com/upload_thumbnail?v=Jwl0gTnk1H0&t=1&ts=1507271796566)](https://www.youtube.com/watch?v=Jwl0gTnk1H0&feature=youtu.be)

+ [http://api.rubyonrails.org/v5.1.4/](http://api.rubyonrails.org/v5.1.4/)
+ [http://guides.rubyonrails.org/active_job_basics.html](http://guides.rubyonrails.org/active_job_basics.html)
