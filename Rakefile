task default: :dev

desc "Run a local development Jekyll instance"
task :dev do
	sh "bundle exec jekyll --server --auto --future --url http://localhost:4000"
end

desc "Push current commit to prod"
task :prod => [:on_main, :clean_git] do
	sh "git push enquowww@enquo.org:app/repo main:master"
end

task :on_main do
	true
end

task :clean_git do
	true
end
