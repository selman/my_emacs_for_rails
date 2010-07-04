require 'fileutils'

task :default => ["update"]

desc "installs my emacs for rails"
task :install do
  puts "preparing \".emacs.d\" directory"
  emacsd = File.join(ENV[:HOME], '.emacs.d')
  if File.exist?(emacsd)
    File.symlink?(emacsd) ? File.unlink(emacsd) : File.rename(emacsd, "#{emacsd}.bak")
  end
  FileUtils.ln_s(Dir.pwd, emacsd)
  FileUtils.cp('init.el', 'init.el.bak') if File.exist?('init.el')
  FileUtils.cp('init.el.example', 'init.el')
  Rake::Task[:update].invoke
end

desc "updates my emacs for rails and submodules"
task :update do
  puts "updating"
  system("git pull")
  puts "updating submodules"
  system("git submodule update --init")
  Rake::Task[:rsense].invoke
end

desc "updates #{ENV[:HOME]}/.rsense run this after every gem install to get new completions"
task :rsense do
  puts "creating .rsense file"
  system("ruby plugins/rsense/etc/config.rb > #{ENV[:HOME]}/.rsense")
end
