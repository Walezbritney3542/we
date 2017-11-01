# we<?php

namespace App\Commands;

use Illuminate\Console\Command;

class DescTableCommand extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'db:desc {table : Table name}';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Desc a database table';

    /**
     * Create a new command instance.
     *
     * @return void
     */
    public function __construct()
    {
        parent::__construct();
    }

    /**
     * Execute the console command.
     *
     * @return mixed
     */
    public function handle()
    {
        $table = $this->argument('table');

        $headers = ['Field', 'Type', 'Null', 'Key', 'Default', 'Extra'];

        $desc = \DB::select("desc ${table};");

        $obj = [];

        for ($i = 0; $i < count($desc); $i++) {
            $obj[$i] = (Array)$desc[$i];
        }

        $this->table($headers, $obj);
    }
}
