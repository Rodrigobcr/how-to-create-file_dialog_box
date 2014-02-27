File Dialog Box
=============================

This ABAP program was created for teaching purposes. His explanation are into this video:

<a href="http://www.youtube.com/watch?v=9U8hDmSWwGw" target="_blank">File Dialog Box</a>


Installation
------------

Copy the coding and paste to your ABAP environment.



FOLLOW CODING BELLOW:

<div class><pre>

**************************VARIÁVEIS PARA O POPUP DE SEEÇÃO DE ARQUIVOS

DATA it_files TYPE filetable.
DATA wa_files TYPE file_table.
DATA v_rc     TYPE i.

*********************** Definição de parametro de seleção
PARAMETERS p_file(1024) TYPE c.

********************* Evento para ativaro matchcode
AT SELECTION-SCREEN ON VALUE-REQUEST FOR p_file.


********************* metodo para exibir o popup de seleção de arquivos
  CALL METHOD cl_gui_frontend_services=>file_open_dialog
    CHANGING
      file_table              = it_files
      rc                      = v_rc
    EXCEPTIONS
      file_open_dialog_failed = 1
      cntl_error              = 2
      error_no_gui            = 3
      not_supported_by_gui    = 4
      OTHERS                  = 5.

  IF sy-subrc NE 0.
    MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
               WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
  ELSE.
************************** identifica o arquivo selecionado e joga para o parametro de seleção
    READ TABLE it_files INTO wa_files INDEX 1.
    p_file = wa_files-filename.
  ENDIF.
  </pre></div>
___________
