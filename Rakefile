
namespace :bootstrap do

  desc 'Download Bootstrap v3.0.0 from Github into _bootstrap'
  task :install => '_bootstrap'
  file '_bootstrap' do |t|
    sh 'wget -q -O - https://github.com/twbs/bootstrap/archive/v3.0.0.tar.gz | tar -xzf -'
    sh "mv bootstrap-3.0.0 #{t.name}"
  end

  desc 'Compile Bootstrap CSS and JavaScript'
  task :generate => [:clean, 'css/bootstrap.css', 'js/bootstrap.js', 'js/html5shiv.js', 'js/respond.min.js']

  file 'css/bootstrap.css' => '_bootstrap' do |t|
    compress = '--compress ' unless ENV['COMPRESS'] == 'NO'
    sh "lessc #{compress}_bootstrap/less/bootstrap.less > #{t.name}"
  end

  file 'js/bootstrap.js' => '_bootstrap' do |t|
    compress = '--compress ' unless ENV['COMPRESS'] == 'NO'
    sh "uglifyjs _bootstrap/js/*.js #{compress}> #{t.name}"
  end

  file 'js/html5shiv.js' => '_bootstrap' do |t|
    sh "cp _bootstrap/assets/#{t.name} #{t.name}"
  end

  file 'js/respond.min.js' => '_bootstrap' do |t|
    sh "cp _bootstrap/assets/#{t.name} #{t.name}"
  end

  directory 'js/bootstrap'

  desc 'Remove generated Bootstrap CSS and JavaScript'
  task :clean => [:clean_css, :clean_js]

  task :clean_css do
    sh 'rm -f css/bootstrap.css'
  end

  task :clean_js do
    sh 'rm -f js/bootstrap.js'
    sh 'rm -f js/html5shiv.js'
    sh 'rm -f js/respond.min.js'
  end
end

namespace :jquery do

  desc 'Download jQuery v1.10.2 into js/jquery.js'
  task :install => 'js/jquery.js'

  file 'js/jquery.js' do |t|
    min = '.min' unless ENV['COMPRESS'] == 'NO'
    sh "wget -q -O #{t.name} http://code.jquery.com/jquery-1.10.2#{min}.js"
  end

  desc "Remove jQuery"
  task :clean do
    sh 'rm -f js/jquery.js'
  end
end
