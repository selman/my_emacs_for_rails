require 'fileutils'

task :default => ["update"]

desc "installs my emacs for rails"
task :install do
  puts "preparing \".emacs.d\" directory"
  emacsd = File.join(ENV[:HOME], '.emacs.d') || nil
  if File.exist?(emacsd)
    File.directory?(emacsd) ? File.rename(emacsd, "#{emacsd}.bak") : File.unlink(emacsd)
  end
  FileUtils.ln_s(Dir.pwd, emacsd)
  FileUtils.cp('init.el.example', 'init.el') unless File.exist?('init.el')
  Rake::Task[:update].invoke
end

desc "updates my emacs for rails and submodules"
task :update do
  puts "updating"
  `git pull`

  puts "updating submodules"
  `git submodule update --init`
end
