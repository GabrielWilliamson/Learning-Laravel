GENERAR PDFS DESDE LARAVEL
Libreria: TCPDF 

asegurese de ingresar al directorio correspondiente de su proyecto
estando en el directorio correcto agregue la dependencia correspondiente

	composer require tecnick.com/tcpdf

puede crear un nuevo controllador en este caso 'pdfController'

en el controlador hacer uso de de la libreria
	use TCPDF;


podemos crear una clase base para agregar los encabezados y el footer
la idea es que sirva como una base para todos sus informes

class MYPDF extends TCPDF{ //esta es una clase base

    public function Header() {  
                
        $texto ='<h1>Esto es un encabezado</h1>';
        $this->writeHTML($texto, true, false, true, false, 'C');      
    } 
    public function Footer() {        
        $this->SetY(-15);        
        $this->Cell(0, 10, 'Page '.$this->getAliasNumPage().'/'.$this->getAliasNbPages(), 
        0, false, 'C', 0, '', 0, false, 'T', 'M');
    } 
}


AGREGUE UN METODO 
class pdfcontroller extends Controller
{
    public function mypdf(){

        $pdf = new MYPDF('L', PDF_UNIT, PDF_PAGE_FORMAT, 
        true, 'UTF-8', false);       
        $pdf->AddPage();           
        $pdf->Output('Prueba.pdf', 'I');
    }
}

AHORA AGREGUE UNA RUTA PARA ACCEDER A A SU PDF 

	Route::get('/pdf', [pdfcontroller::class,'mypdf' ]);


