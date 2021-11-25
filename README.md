# Exemplo de função onde primeiro passo um parâmetro de filtragem, e depois somo os valore de uma coluna específica do banco.

## Depois que estiver com toda a sua estrutura montada (migrations, model, api, controller), no seu arquivo de controller, crie uma function da seguinte forma.

```
public function countValortotal(Request $request)
{
    try {
        $total = DB::table("pedidos")->where('status_venda', ['Vendido'])
                                    ->get()
                                    ->sum("price");
        return $this->getResponseJson($total, 'sucess', '', [], Response::HTTP_OK);
    } catch (ValidationException $validationException) {
        return $this->getResponseJson([], 'error', $validationException->getMessage(), [], Response::HTTP_UNPROCESSABLE_ENTITY);
    } catch (\Exception $exception) {
        return $this->getResponseJson([], 'error', $exception->getMessage(), [], Response::HTTP_INTERNAL_SERVER_ERROR);
    }
}
```

# Nesse exemplo podemos ver que primeiro, se usa o helper DB instanciando a tabela que vamos usar ("pedidos") o where estou usando para filtrar pedidos que tenham apenas o 'status_venda' = 'Vendido', e em seguida uso o ->sum (É uma método que faz a soma de todos os valores de uma coluna, no caso a "price").


