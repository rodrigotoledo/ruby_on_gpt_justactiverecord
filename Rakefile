require 'bundler/setup'
require 'active_record'
require 'pg'
require 'yaml'

namespace :db do
  task :load_config do
    db_config = YAML.safe_load(File.read('config/database.yml'))
    ActiveRecord::Base.establish_connection(db_config.symbolize_keys[:development])
  end

  desc 'Create the users table'
  task create_users_table: :load_config do
    ActiveRecord::Schema.define do
      create_table :users do |t|
        t.string :name
        t.string :email, unique: true
      end
    end
  end

  desc 'Add the age column to the users table'
  task add_age_column: :load_config do
    ActiveRecord::Base.connection.add_column :users, :age, :integer
  end
end
