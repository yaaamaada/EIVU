
CACHELINE_SIZE = 64

agsz = get_option('aggregation_num')
md = get_option('metadata_size')
mdbufsz = md * agsz
if mdbufsz % 64 != 0
    mdbufsz += CACHELINE_SIZE - md * agsz % CACHELINE_SIZE
endif
mdbufnum = 2048 / agsz * 32
if mdbufnum % 64 != 0
    mdbufnum += CACHELINE_SIZE - (2048 / agsz * 32) % CACHELINE_SIZE
endif

add_global_arguments(f'-DAGGREGATED_MD_NUM=@agsz@', language : 'c')
add_global_arguments(f'-DMDBUF_SIZE=@mdbufsz@', language : 'c')
add_global_arguments(f'-DMDBUF_NUM=@mdbufnum@', language : 'c')

if get_option('aggregated_md')
    if get_option('reuse')
        args_guest += '-DMD_MEMOBJ_CACHE_STACK'
        incdir_guest += include_directories('reuse')
    else
        args_guest += '-DMD_MEMOBJ_CACHE_STACK'
        incdir_guest += include_directories('mpool')
    endif
endif

if get_option('host_aggregated_md')
    if get_option('reuse')
        args_host += '-DMD_MEMOBJ_CACHE_STACK'
        incdir_host += include_directories('reuse')
    else
        args_host += '-DMD_MEMOBJ_CACHE_STACK'
        incdir_host += include_directories('mpool')
    endif
endif
