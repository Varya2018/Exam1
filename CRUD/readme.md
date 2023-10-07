1. вывод данных из бд
2. представление плиткой(часто 1 стр под каждый вывод)
3. за таблицу отвечает grid , за плитку listView
 Алгоритм:
для получения данных нужно создать context


 public static rulEntities Context;

        public static rulEntities GetContext()
        {
            if (Context == null)
            {
                Context = new Models.rulEntities();
            }
            return Context; 
        }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            throw new UnintentionalCodeFirstException();
        }



  вторая строка нужна будет для кнопок добавить/удалить

  данные из таблицы - datagrid имя обычно включает DG или из таблицы из которой берём данные

      <DataGrid Name="DGUsers" AutoGenerateColumns ="False"  >
            <DataGrid.Columns >
                <DataGridTextColumn Header="№" Binding ="{Binding ID}" Width="auto"></DataGridTextColumn>
                <DataGridTextColumn Header="Тип" Binding ="{Binding Type}" Width="auto"></DataGridTextColumn>
                <DataGridTextColumn Header="Логин" Binding ="{Binding Login}" Width="auto"></DataGridTextColumn>
                <DataGridTextColumn Header="Пароль" Binding ="{Binding Password}" Width="auto"></DataGridTextColumn>
                <DataGridTemplateColumn>
                    <DataGridTemplateColumn.CellTemplate>
                        <DataTemplate>
                            <Button Name ="edit" Click="EditClick"></Button>
                        </DataTemplate>
                    </DataGridTemplateColumn.CellTemplate>
                </DataGridTemplateColumn>
            </DataGrid.Columns>



   структура столбца:
   заголовок(предпочтительно на русском), указание на столбец таблицы(), ширина( Header="Пароль" Binding ="{Binding Password}" Width="auto")



   Вывод данных: название DG, элементы, название папки, название бд, функция для получения контекста, таблица и список

           DGUsers.ItemsSource = Models.rulEntities.GetContext().Datas.ToList();
        
            
