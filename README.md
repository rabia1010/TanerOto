# Bootstrap yapma

İlk olarak bootstrap dizinini masaüstüne indiriyoruz. 

Bootstrap dizininin içinde bulunan tüm .css uzantılı dosyalar app/assets/stylesheets içine atılır.

app/assets/stylesheets/application.css içindeki,
```css
 *= require_tree .
 *= require_self
```
ilk satır tüm css dosyalarının tanınmasını sağlayacaktır.

Daha sonra bootstrap dizinindeki .js uzantılı dosyalarının hepsi app/assets/javascripts içine atılır.

gemfile içine aşağıdaki gem dahil edilir ve bundle edilir.

```ruby
gem 'jquery-rails', '~> 4.3', '>= 4.3.1'
```

app/assets/javascripts/application.js dosyasının içi aşağıdaki gibi görünecektir.
```js
//= require jquery2
//= require jquery_ujs
//= require rails-ujs
//= require_tree .
```

Daha sonra bootstraptaki tüm js'lerin tanınması için ilk olarak app/views/layouts/application.html.erb içindeki 'head' bloğu(kullandığımız bootstrap için js'ler dahil edilmiştir.) aşağıdaki gibi görünecektir
```html
<head>
    <title>TanerOto</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'bootstrap-select.min', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'bootstrap-slider', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'bootstrap-submenu', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'bootstrap.min', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'wow.min', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'ie-emulation-modes-warning', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'ie10-viewport-bug-workaround', 'data-turbolinks-track': 'reload' %>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>
```

Bu da yeterli olmayacaktır. Çünkü .js uzantılı dosyaların derlenmesi gerekmektedir. bunu da tüm js dosyalarını tek tek derleyecek olan bir yöntemle yapıyoruz. config/initializers/assets.rb içine aşağıdaki satırları ekliyoruz.
```ruby
Rails.application.config.assets.precompile += %w( app.js )
Rails.application.config.assets.precompile += %w( bootstrap-select.min.js )
Rails.application.config.assets.precompile += %w( bootstrap-slider.js )
Rails.application.config.assets.precompile += %w( bootstrap-submenu.js )
Rails.application.config.assets.precompile += %w( bootstrap.min.js )
Rails.application.config.assets.precompile += %w( wow.min.js )
Rails.application.config.assets.precompile += %w( ie-emulation-modes-warning.js )
Rails.application.config.assets.precompile += %w( ie10-viewport-bug-workaround.js )
```

Bu sayede bootstrapı projemize dahil etmiş olduk. Sırada sayfaların ayarlanması var bunun için bir controller oluşturulur:
```bash
$ rails g controller pages index contact
```
pages kontrolörünün index ve contact adında iki sayfası olur. Sayfa içerikleri app/views/index.html.erb ve contact.html.erb içindedir. Bu içerikler yine bootstrap dizinindeki index.html ve contact.html den alınır.





