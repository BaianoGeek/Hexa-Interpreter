def interpret_hexa(hex_data):

    #ETHERNET
    dst_mac       = hex_data[:12]
    src_mac       = hex_data[12:24]
    protocol_type = hex_data[24:28]

    #IP
    ip_version    = int(hex_data[28:29])
    header_length = int(hex_data[29:30]) * ip_version
    full_size     = int(hex_data[32:36], 16)
    ttl           = int(hex_data[44:46], 16)
    protocol      = hex_data[46:48]
    src_ip        = hex_data[52:60]
    dst_ip        = hex_data[60:68]

    #TCP
    src_port = int(hex_data[68:72], 16)
    dst_port = int(hex_data[72:76], 16)
    flags    = int(hex_data[94:96], 16)

    flag_names = {
        1: "FIN",
        2: "SYN",
        4: "RST",
        8: "PSH",
        16: "ACK",
        32: "URG"
    }
    active_flag_names = ", ".join(flag_names[flag] for flag in flag_names if flags & flag)

    #Convertendo de Hexadecimal para decimal cada Byte
    src_ip = ".".join(str(int(hex_data[i:i+2], 16)) for i in range(52, 60, 2))
    dst_ip = ".".join(str(int(hex_data[i:i+2], 16)) for i in range(60, 68, 2))
    
    return dst_mac, src_mac, protocol_type, ip_version, header_length, full_size, ttl, protocol, src_ip, dst_ip, src_port, dst_port, flags, active_flag_names

def extract_payload(hex_data):
    flags_byte = int(hex_data[92:94], 16)
    tcp_header_length = (flags_byte >> 4) * 4

    payload_hex = hex_data[tcp_header_length * 2:]
    payload_ascii = bytearray.fromhex(payload_hex).decode(errors='ignore')
    
    return payload_ascii

def main():
    hex_data = input("Digite o hexadecimal: \n").strip()

    if not hex_data: 
        print("Nenhum valor foi fornecido. Encerrando Interpretador.") 
        return

    # Verifica se há espaços e remove, se necessário
    hex_data = hex_data.replace(" ", "")

    # Interpretação Ethernet
    dst_mac, src_mac, protocol_type, ip_version, header_length, full_size, ttl, protocol, src_ip, dst_ip, src_port, dst_port, flags, active_flag_names = interpret_hexa(hex_data)
    print("\n====================ETHERNET====================\n")
    print("Mac de Destino   \t", ":".join([dst_mac[i:i+2] for i in range(0, len(dst_mac), 2)]))
    print("Mac de Origem    \t", ":".join([src_mac[i:i+2] for i in range(0, len(src_mac), 2)]))
    print("Tipo de Protocolo\t", " ".join([protocol_type[i:i+2] for i in range(0, len(protocol_type), 2)]))

    print("\n=======================IP=======================\n")
    print("Versão                \tIPv" + str(ip_version))
    print("Tamanho do Cabeçalho  \t" + str(header_length))
    print("Tamanho tot. do pacote\t" + str(full_size))
    print("TTL                   \t" + str(ttl))
    print("Protocolo             \t" + protocol)
    print("IP de Origem          \t" + src_ip)
    print("IP de Destino         \t" + dst_ip)

    print("\n=======================TCP======================\n")
    print("Porta de Origem       \t" + str(src_port))
    print("Porta de Destino      \t" + str(dst_port))
    print("Flags                 \t" + str(flags) + " : " + active_flag_names)

    payload_ascii = extract_payload(hex_data)
    print("\n====================Payload====================\n")
    print(payload_ascii)


if __name__ == "__main__":
    main()
