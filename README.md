# epsonTMT20
Library to connect EPSON TM-T20 thermal print with software

## Delphi

#Include "Fivewin.Ch"
 
STATIC XDLL_EPSON  //-> DLL DA IMPRESSORA FISCAL EPSON TMT81
 
/*****************************************************************************/
/* Declaração de funções da DLL 32 Bits para cupom fiscal TMT81              */
/*****************************************************************************/
// Abre porta de comunicacao
 
DLL32 FUNCTION EpAbrPorCo(Veloc    AS PTR,;
                          Port     AS PTR) AS LONG PASCAL;
      FROM "EPSON_Serial_Abrir_Porta"       LIB XDLL_EPSON
 
// Fecha porta de comunicacao
DLL32 FUNCTION EpFecPorCo(             ) AS LONG PASCAL;
      FROM "EPSON_Serial_Fechar_Porta"      LIB XDLL_EPSON
 
// EFetua recebimento nao fiscal MFD
DLL32 FUNCTION EpEfRcNFMFD( vNroOp       AS LPSTR,;
                            vVlrOp       AS LPSTR,;
                            nCasDec      AS   PTR ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Vender_Item"                 LIB XDLL_EPSON
 
// Fecha Comprovante nao Fiscal
DLL32 FUNCTION EpFcRecNfMF( OpCortaPapel     AS BOOL ) AS LONG PASCAL ;
      FROM "EPSON_NaoFiscal_Fechar_Comprovante" LIB XDLL_EPSON
 
// Verifica Corte Gilhotina
DLL32 FUNCTION EpVerCorGui( @ST1          AS BOOL   ) AS LONG PASCAL;
      FROM "EPSON_Obter_Estado_Corte_Papel"              LIB XDLL_EPSON
 
// Ativa Corte Gilhotina
DLL32 FUNCTION EpAtvCrtCup( lOpCorPap      AS BOOL  ) AS LONG PASCAL;
      FROM "EPSON_Config_Corte_Papel"                    LIB XDLL_EPSON
 
// cancelamento recebimento
DLL32 FUNCTION EpCanRecNFs(                         ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Cancelar_Comprovante" LIB XDLL_EPSON
 
// Programa um caracter gráfico para autenticação
DLL32 FUNCTION EpPrgCrAut( vDadLog          AS LPSTR,;
                           nTamCam             AS PTR,;
                           nLinha1          AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Config_Logotipo" LIB XDLL_EPSON
 
// Cancela impressão de cheque
DLL32 FUNCTION EpCanImChq(                         ) AS LONG PASCAL ;
      FROM "EPSON_Cheque_Cancelar_Impressao" LIB XDLL_EPSON
 
// Nomeia Totalizadores Nao fiscais
DLL32 FUNCTION EpNomToNSI( vDesTot     AS LPSTR,;
                           @nIdTot      AS   PTR) AS LONG PASCAL ;
      FROM "EPSON_Config_Totalizador_NaoFiscal" LIB XDLL_EPSON
 
// Retorna os dados da impressora no momento da última Redução Z
DLL32 FUNCTION EpDadUlRed( vUltRed         AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_Obter_Dados_Ultima_RZ"                 LIB XDLL_EPSON
 
// Programa os espacamentos de linhas entre os cupons
DLL32 FUNCTION EpVerLECup( EspCup    AS LPSTR      ) AS LONG PASCAL;
      FROM "EPSON_Config_Espaco_Entre_Documentos"      LIB XDLL_EPSON
 
// Programa os espacamento entre as linhas no cupom
DLL32 FUNCTION EpVerEsLin( vEspLin         AS LPSTR    ) AS LONG PASCAL;
      FROM "EPSON_Config_Espaco_Entre_Linhas"               LIB XDLL_EPSON
 
//Programa o nome da moeda no singular e no plural para a expresão em cheque
DLL32 FUNCTION EpPrgMoSin( vSing         AS LPSTR,;
                           vPlural       AS LPSTR) AS LONG PASCAL ;
      FROM "EPSON_Cheque_Configurar_Moeda"            LIB XDLL_EPSON
 
//Programa Aliquota ECF
DLL32 FUNCTION EpProAlEcf( Valor           AS LPSTR,;
                           IssIcms         AS BOOL    ) AS LONG PASCAL;
      FROM "EPSON_Config_Aliquota"                          LIB XDLL_EPSON
 
//Recebe os dados da Leitura X pela serial e grava em arquivo texto
DLL32 FUNCTION EpLeiLXSer( vDiretorio   AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_RelatorioFiscal_Salvar_LeituraX"    LIB XDLL_EPSON
 
//Numero de Interverções Fiscais
DLL32 FUNCTION EpNumInFis( Intervencoes AS LPSTR   ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Contadores"                 LIB XDLL_EPSON
 
//Imprimi Cheque
DLL32 FUNCTION EpImChqEcf( vNroReg     AS LPSTR,;
                           vValor      AS LPSTR,;
                           nCasDec       AS PTR,;
                           vNominal    AS LPSTR,;
                           vCidade     AS LPSTR,;
                           vData       AS LPSTR,;
                           vTextoAd    AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Cheque_Imprimir" LIB XDLL_EPSON
 
//Programa horario de verao
DLL32 FUNCTION EpPrgHrVer(         )  AS LONG PASCAL;
      FROM "EPSON_Config_Horario_Verao" LIB XDLL_EPSON
 
//Obtem horario de verao
DLL32 FUNCTION EpEstHorVer( @lEstHrVer   AS PTR )  AS LONG PASCAL;
      FROM "EPSON_Obter_Estado_Horario_Verao"           LIB XDLL_EPSON
 
//Autentica Documentos
DLL32 FUNCTION EpAutDcEcf( vTexto      AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Autenticar_Imprimir" LIB XDLL_EPSON
 
//Retorna Moeda Corrente
DLL32 FUNCTION EpSimMoCur( vMoeda     AS LPSTR    ) AS LONG PASCAL;
      FROM "EPSON_Obter_Simbolo_Moeda"                 LIB XDLL_EPSON
 
// Verifica Qtd Casas Decimais
DLL32 FUNCTION EpVerCasD( vCasDec        AS LPSTR  ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Casas_Decimais" LIB XDLL_EPSON
       
 
//Retorna CGC e Inscricao Estadual do Cliente
DLL32 FUNCTION EpCgcIECli( vDadosCli         AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Dados_Usuario" LIB XDLL_EPSON
 
// Identificação do Consumidor
DLL32 FUNCTION EpIdeCoCup( vCNPJ        AS LPSTR,;
                           vNome        AS LPSTR,;
                           vEnd1        AS LPSTR,;
                           vEnd2        AS LPSTR,;
                           nOpImp       AS   PTR ) AS LONG PASCAL;
      FROM "EPSON_Fiscal_Dados_Usuario"               LIB XDLL_EPSON
 
//Cancela item generico
DLL32 FUNCTION EpCanItGen( NroIte      AS LPSTR     ) AS LONG PASCAL;
      FROM "EPSON_Fiscal_Cancelar_Item"                  LIB XDLL_EPSON
//Vende ítem
DLL32 FUNCTION EpVendItem( Codigo      AS LPSTR,;
                           Descricao   AS LPSTR,;
                           Quantid     AS LPSTR,;
                           CasDecQtd   AS   PTR,;
                           Unidade     AS LPSTR,;
                           ValUnit     AS LPSTR,;
                           CasDecVlr   AS   PTR,;
                           Aliquota    AS LPSTR,;
                           QtdLinha    AS   PTR ) AS LONG PASCAL;
      FROM "EPSON_Fiscal_Vender_Item"               LIB XDLL_EPSON
 
//Efetua Forma de Pagamento com ID da Forma
DLL32 FUNCTION EpEfeFrPgd( IdPgt         AS LPSTR,;
                           VlrPgt        AS LPSTR,;
                           NroCas          AS PTR,;
                           Linha1        AS LPSTR,;
                           Linha2        AS LPSTR        ) AS LONG PASCAL;
      FROM "EPSON_Fiscal_Pagamento"                           LIB XDLL_EPSON
 
//Verifica ultimo item vendido
DLL32 FUNCTION EpUltItVen( vRet1       AS LPSTR     ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Numero_Ultimo_Item"              LIB XDLL_EPSON
 
// Programa Forma de Pagamento
DLL32 FUNCTION EpProgFpgt( VincNvinc       AS BOOL,;
                           IdFrmPgt        AS LPSTR,;
                           DescFrmPgto     AS LPSTR    ) AS LONG PASCAL ;
      FROM "EPSON_Config_Forma_Pagamento" LIB XDLL_EPSON
 
//Verifica a retorno aliquotas
DLL32 FUNCTION EpVerReAlq( Aliquotas   AS LPSTR   ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Tabela_Aliquotas" LIB XDLL_EPSON
 
//Verifica a versão do firmware
DLL32 FUNCTION EpVerFiWar( vRet1       AS LPSTR     ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Dados_Impressora" LIB XDLL_EPSON
 
//Verifica o numero de serie da ecf e MFD
DLL32 FUNCTION EpVerNuSer( ST1       AS LPSTR   ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Dados_Impressora" LIB XDLL_EPSON
 
//Recebimento não fiscal MFD
DLL32 FUNCTION EpEfeRnfMf( vCNPJ         AS LPSTR,;
                           vRazao        AS LPSTR,;
                           vEnd1         AS LPSTR,;
                           vEnd2         AS LPSTR,;
                           nOpCab        AS   PTR   ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Abrir_Comprovante"     LIB XDLL_EPSON
 
//Verifica o status da impressora
DLL32 FUNCTION EpVerStImp( Resposta AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Estado_Impressora"        LIB XDLL_EPSON
       
//Verifica o status do ultimo comando     
DLL32 FUNCTION EpStUltCmd( CodErr  AS LPSTR,;
                           RespErr AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Mensagem_Erro"           LIB XDLL_EPSON
 
//Ler total do cupom
DLL32 FUNCTION EpSubTotal( SubTotal    AS STRING  ) AS LONG PASCAL ;
      FROM "EPSON_Fiscal_Obter_SubTotal"                 LIB XDLL_EPSON
 
//Ler número do caixa
DLL32 FUNCTION EpNumeroCx( NumeroCaixa AS LPSTR     ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Numero_ECF_Loja" LIB XDLL_EPSON
 
//Ler data do movimento
DLL32 FUNCTION EpDtMovto(DtHrMovto     AS LPSTR) AS LONG PASCAL ;
      FROM "EPSON_Obter_Data_Hora_Jornada"          LIB XDLL_EPSON
 
//Ler data e hora da impressora
DLL32 FUNCTION EpDtHora( DtHs AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_Obter_Hora_Relogio"       LIB XDLL_EPSON
 
//Ler Status do Movimento
DLL32 FUNCTION EpObEstImp( Status AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_Obter_Dados_Jornada"      LIB XDLL_EPSON
//Inicia Dia
DLL32 FUNCTION EpAbrDiaFi( )            AS LONG PASCAL ;
      FROM "EPSON_RelatorioFiscal_Abrir_Dia" LIB XDLL_EPSON
//Ler flag fiscal da impressora e de documentos não fiscal   
DLL32 FUNCTION EpFlagFisc( @FlagFiscal AS LPSTR   ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Estado_Cupom" LIB XDLL_EPSON
 
//Emite leitura X
DLL32 FUNCTION EpLeituraX(             ) AS LONG PASCAL;
      FROM "EPSON_RelatorioFiscal_LeituraX" LIB XDLL_EPSON
 
//Emite redução Z
DLL32 FUNCTION EpReducaoZ(  vData           AS LPSTR,;
                            vHoras          AS LPSTR,;
                            nOpHorVer       AS   PTR,;
                            vCRZ             AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_RelatorioFiscal_RZ" LIB XDLL_EPSON
 
//Abre cupom fiscal
DLL32 FUNCTION EpAbreCup ( CNPJ              AS LPSTR,;
                           Razao             AS LPSTR,;
                           End1              AS LPSTR,;
                           End2              AS LPSTR,;
                           OpImpCli          AS    PTR ) AS LONG PASCAL ;
      FROM "EPSON_Fiscal_Abrir_Cupom" LIB XDLL_EPSON
 
//Verifica se tem impressora ligada
DLL32 FUNCTION EpPrintLig(           ) AS LONG PASCAL;
      FROM "EPSON_Serial_Obter_Estado_Com" LIB XDLL_EPSON
 
//Cancela cupom fiscal
DLL32 FUNCTION EpCanCupom(                       ) AS LONG PASCAL;
      FROM "EPSON_Fiscal_Cancelar_Cupom"             LIB XDLL_EPSON
 
//Cancela Comprovante de Credito Debito (Cupom Vinculado)
DLL32 FUNCTION EpCanCcdNf( vIdFrmPgt        AS LPSTR,;
                           vVllrPgt         AS LPSTR,;
                           nCasDec          AS   PTR,;
                           vNroParc         AS LPSTR,;
                           vNroCup          AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Cancelar_CCD"              LIB XDLL_EPSON
 
//Retorna Informação sobre ultimo documento
DLL32 FUNCTION EpInfUtDoc( vUltDoc    AS LPSTR ) AS    LONG PASCAL;
      FROM "EPSON_Obter_Informacao_Ultimo_Documento"  LIB XDLL_EPSON
 
//Cancela último ítem do cupom
DLL32 FUNCTION EpCancItem(                          ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Cancelar_Ultimo_Item"        LIB XDLL_EPSON
 
//Ler número do cupom
DLL32 FUNCTION EpNumCupom( Cupom       AS LPSTR     ) AS LONG PASCAL ;
      FROM "EPSON_Obter_Contadores"                      LIB XDLL_EPSON
 
//Emite cupom gerencial
DLL32 FUNCTION EpCpGerAbr( Texto AS LPSTR            ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Abrir_Relatorio_Gerencial"    LIB XDLL_EPSON
 
//Fecha cupom gerencial
DLL32 FUNCTION EpCpGerFec(   OpCortar  AS  BOOL         ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Fechar_CCD"                  LIB XDLL_EPSON
 
//Abre a gaveta
DLL32 FUNCTION EpAbreGav (                          ) AS LONG PASCAL ;
      FROM "EPSON_Impressora_Abrir_Gaveta"             LIB XDLL_EPSON
 
//Abre cupom adicional
DLL32 FUNCTION EpCupAdAbr( vIdFormaPgto   AS LPSTR,;
                           vValor         AS LPSTR,;
                           nNroCas        AS   PTR,;
                           vNroPar        AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Abrir_CCD"               LIB XDLL_EPSON
 
// Imprime cupom não fiscal vinculado
DLL32 FUNCTION EpCupAdUsa( Texto       AS LPSTR ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Imprimir_LinhaEX"       LIB XDLL_EPSON
 
// Fecha Comprovante de Credito Debito
DLL32 FUNCTION EpCupAdFec( lOpCorPap AS BOOL    ) AS LONG PASCAL;
      FROM "EPSON_NaoFiscal_Fechar_CCD"              LIB XDLL_EPSON
 
//Fecha Cupom
DLL32 FUNCTION EpFechaCup( CortaPapel  AS BOOL,;
                           ImpCupAd    AS BOOL ) AS LONG PASCAL ;
       FROM "EPSON_Fiscal_Fechar_Cupom"    LIB XDLL_EPSON
 
// Imprime Menssagem no fechamento cupom
DLL32 FUNCTION EpTerFeCup( Linha1    AS LPSTR,;
                           Linha2    AS LPSTR,;
                           Linha3    AS LPSTR,;
                           Linha4    AS LPSTR,;
                           Linha5    AS LPSTR,;
                           Linha6    AS LPSTR,;
                           Linha7    AS LPSTR,;
                           Linha8    AS LPSTR ) AS LONG PASCAL;
       FROM "EPSON_Fiscal_Imprimir_Mensagem"       LIB XDLL_EPSON
        
// Imprime Menssagem de Aplicação
DLL32 FUNCTION EpMsgApl(   Linha1    AS LPSTR,;
                           Linha2    AS LPSTR  ) AS LONG PASCAL;
       FROM "EPSON_Fiscal_Mensagem_Aplicacao"       LIB XDLL_EPSON
 
// Efetua o Download de um cupom do Memoria Fiscal
DLL32 FUNCTION EpDwnCuMfd( vCOO1       AS LPSTR,;
                           vCOO2       AS LPSTR,;
                           nOpEnt        AS PTR,;
                           nOpImp        AS PTR,;
                           nAtoCotep     AS PTR,;
                           nOPSintegra   AS PTR,;
                           vArqSaid    AS LPSTR ) AS LONG PASCAL ;
       FROM "EPSON_Obter_Dados_MF_MFD" LIB XDLL_EPSON
 
// Acrescimo ou Desconto no item.
DLL32 FUNCTION EpEfeAcDes( VlrDesAcr   AS LPSTR,;
                          CasDec       AS PTR,;
                          DesAcr       AS BOOL,;
                          PorVlr       AS BOOL ) AS LONG PASCAL ;
       FROM "EPSON_Fiscal_Desconto_Acrescimo_Item" LIB XDLL_EPSON
 
// Acrescimo ou Desconto no Cupom
DLL32 FUNCTION EpEfeAcDesCup(VlrDesAcr AS LPSTR,;
                             CasDec       AS PTR,;
                             DesAcr       AS BOOL,;
                             PorVlr       AS BOOL   ) AS LONG PASCAL;
       FROM "EPSON_Fiscal_Desconto_Acrescimo_Subtotal" LIB XDLL_EPSON
 
// Efetua Forma de Pagamento Não Fiscal
DLL32 FUNCTION EpEfFPgNf( vIDPgt      AS LPSTR,;
                          vValor      AS LPSTR,;
                          nCasDec       AS PTR,;
                          vLinha1     AS LPSTR,;
                          vLinha2     AS LPSTR ) AS LONG PASCAL ;
      FROM "EPSON_NaoFiscal_Pagamento" LIB XDLL_EPSON
 
//Leitura da memoria fiscal serial por DATA Serial MFD Ou Por Reduçoes
DLL32 FUNCTION EpLeiMfdDt( vData1      AS LPSTR,;
                           vData2      AS LPSTR,;
                           nTipImp     AS   PTR,;
                           vRetorno    AS LPSTR,;
                           vNomArq     AS LPSTR,;
                           nNroByt     AS   PTR,;
                           nBuffer     AS   PTR  ) AS LONG PASCAL ;
      FROM "EPSON_RelatorioFiscal_Leitura_MF" LIB XDLL_EPSON
 
//Retornar o Totalizador Geral
DLL32 FUNCTION EpRetGraTo( vRetTotal  AS LPSTR ) AS LONG PASCAL ;
       FROM "EPSON_Obter_GT"    LIB XDLL_EPSON
 
/// Fim TMT81
